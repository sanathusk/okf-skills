# OKF Cross-linking Rules

Concepts MAY link to other concepts using standard markdown links. Two forms are supported:

## Link Forms

### Absolute (bundle-relative) — RECOMMENDED

Begins with `/`, interpreted relative to the bundle root. This is the **recommended** form because it is stable when documents are moved within their subdirectory.

```markdown
See the [customers table](/tables/customers.md) for the join key.
```

### Relative

A standard markdown relative path.

```markdown
See the [neighboring concept](./other.md).
```

## Path-valued Fields

Several fields name a path or URI: `resource`, `sources[].resource`, `computation`, `executor.resource`, and `attester.resource`. Each path-valued field accepts:

- An absolute URL (for example `https://...`)
- A bundle-relative path beginning with `/`
- A relative path (for example `../computations/revenue.md`)

## Relationship Semantics

A link from concept A to concept B asserts a *relationship*. The specific kind (parent/child, references, joins-with, depends-on) is conveyed by the surrounding prose, not by the link itself.

## Broken Links

Consumers MUST tolerate broken links: a link whose target does not exist in the bundle is not malformed; it may simply represent not-yet-written knowledge.

## The `references/` Convention

A `references/` subdirectory conventionally mirrors external material, run instructions, or code as first-class concepts within the bundle. Sources, executors, and attesters commonly point into it (for example `references/attesters/revenue.py`). It is a naming convention, not a requirement.