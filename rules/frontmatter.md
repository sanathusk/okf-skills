# OKF Frontmatter Field Definitions

Every concept is a UTF-8 markdown file with two parts: a YAML frontmatter block and a markdown body.

## Core Fields (all concepts)

| Field | Required? | Description |
|-------|-----------|-------------|
| `type` | **YES** | Kind of concept (free-form string, e.g. `BigQuery Table`, `Metric`, `Playbook`, `Attested Computation`) |
| `title` | Recommended | Human-readable display name |
| `description` | Recommended | One-sentence summary |
| `resource` | Recommended | URI identifying the underlying asset (omit for abstract concepts) |
| `tags` | Optional | YAML list for cross-cutting categorization |

**Key rules:**
- `type` is the only always-required key; a concept carrying just `type` is fully conformant.
- Type values are **not** registered centrally. Producers SHOULD pick values that are descriptive and self-explanatory.
- Consumers MUST tolerate unknown types gracefully, typically by treating them as generic concepts.

## Trust & Lifecycle Fields (v0.2)

| Field | Required? | Description |
|-------|-----------|-------------|
| `generated` | Optional | `{ by: <actor>, at: <ISO8601> }` — Who/what created this content and when |
| `verified` | Optional | List of `{ by: <actor>, at: <ISO8601> }` — Who confirmed correctness |
| `status` | Optional | `draft` \| `stable` \| `deprecated` — Default: `stable` |
| `stale_after` | Optional | ISO 8601 datetime — Content is stale on/after this instant |

**Key rules:**
- `generated.by`: REQUIRED within `generated`. An actor (see [actor-convention.md](actor-convention.md)).
- `generated.at`: An ISO 8601 datetime marking the content's last meaningful change.
- `verified`: A list of verification events, each with `by` (an actor) and `at` (an ISO 8601 datetime).
- A single verifier MAY be written as one `{ by, at }` mapping without the list dash. Consumers MUST treat a bare mapping as a one-element list.
- `status`: `draft` (not yet reviewed), `stable` (ready for consumption, default), `deprecated` (kept for links and history).
- `stale_after`: An absolute instant. A concept is stale when `now >= stale_after`.

## Provenance Fields (v0.2)

| Field | Required? | Description |
|-------|-----------|-------------|
| `sources` | Optional | List of source entries |
| `usage_window` | Optional | `{ from, to }` — Time range for `usage_count` signals |

Each `sources` entry:
- `resource` (REQUIRED): URL, bundle-relative path, or scope descriptor
- `id`: Stable key for footnote attribution
- `title`: Human-readable label
- `author`: Actor who produced the source
- `usage_count`: How often exercised (liveness signal)
- `last_modified`: When the source last changed

## Attested Computation Fields (v0.2)

For concepts with `type: Attested Computation`:

| Field | Description |
|-------|-------------|
| `runtime` | REQUIRED. How to run it: `bigquery`, `postgres`, `dbt`, `python`, `Looker` |
| `parameters` | List of `{ name, type, required }` — Typed holes the agent fills |
| `computation` | Path to computation file (if not inline in body) |
| `executor` | `{ resource, receipt: [...] }` — How to run and what evidence to capture |
| `attester` | `{ resource }` — Deterministic code that verifies the receipt |

**Key rules:**
- `runtime` is REQUIRED for Attested Computation concepts.
- Agent fills parameters only — never edits the computation itself.
- Computation can be inline (body under `# Computation`) or external (`computation` field).

## Extensions

Producers MAY include any additional keys. Consumers SHOULD preserve unknown keys when round-tripping and MUST NOT reject documents with unrecognized fields.