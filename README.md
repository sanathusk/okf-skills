[![skills.sh](https://skills.sh/b/okf-skills)](https://skills.sh/okf-skills)

# OKF Skills

An [Agent Skill](https://agentskills.io) for the [Open Knowledge Format](https://github.com/GoogleCloudPlatform/open-knowledge-format) (OKF) — the open spec for representing organizational knowledge as markdown files with YAML frontmatter.

## About OKF

OKF is a vendor-neutral, open spec (v0.2, released by Google Cloud) for representing knowledge as a directory of markdown files with YAML frontmatter. No SDK required — if you can `cat` a file, you can read OKF.

It formalizes the "LLM Wiki" pattern ([Karpathy's gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)) into an interoperable format: wikis written by different producers can be consumed by different agents without translation.

**v0.2 adds:** provenance tracking (`sources`), trust signals (`generated`, `verified`), lifecycle management (`status`, `stale_after`), and **Attested Computations** — a new concept type for sanctioned, verifiable calculations.

## Available Skill

### OKF — Open Knowledge Format · `library-and-api-reference`

Create, validate, and enrich OKF bundles. Includes bash validator, conversion guides (Notion, Obsidian, CSV), and integration with Google Cloud Knowledge Catalog via kcmd CLI/MCP.

**When to use:** create OKF bundles, validate conformance, enrich concepts with schema/citations/cross-links, convert existing knowledge (Notion exports, Obsidian vaults, spreadsheets) to OKF, structure a knowledge base for AI agent consumption, generate `index.md` and `log.md` files, push bundles to Knowledge Catalog via kcmd.

**Key features:**

- **Bundle creation** — scaffold conformant directories with `index.md`, `log.md`, and concept files
- **v0.2 frontmatter** — trust fields (`generated`, `verified`), lifecycle (`status`, `stale_after`), provenance (`sources`)
- **Attested Computations** — concepts that carry sanctioned, verifiable calculations with executor/attester patterns
- **Validation** — built-in bash validator + integration with [okflint](https://github.com/mattdav/okflint) (18-rule Python linter)
- **Conversion** — guides for migrating Notion, Obsidian, and CSV/ spreadsheets to OKF
- **Google Cloud integration** — serve via Knowledge Catalog using kcmd CLI or MCP server

📄 [View full documentation](skills/okf-open-knowledge-format/SKILL.md) | 🌐 [okf.md](https://okf.md) | 📘 [OKF Spec v0.2](https://github.com/GoogleCloudPlatform/open-knowledge-format/blob/main/okf/SPEC.md)

## Installation

### Via [Skills.sh](https://skills.sh/docs)

```bash
npx skills add https://github.com/okf-skills/okf-skills
```

Or install directly:

```bash
npx skills add https://github.com/okf-skills/okf-skills -s okf-open-knowledge-format
```

### Manual Installation

1. Clone this repository:
```bash
git clone https://github.com/okf-skills/okf-skills.git
```

2. Copy the skill folder to your agent's skills directory:
```bash
# Example for Cursor
cp -r skills/okf-open-knowledge-format .cursor/skills/

# Example for Claude Code
cp -r skills/okf-open-knowledge-format .claude/skills/

# Example for Kiro
cp -r skills/okf-open-knowledge-format .kiro/skills/
```

The Agent Skills format is universal and works with any compatible agent. See the [official specification](https://agentskills.io/specification.md) for details.

## Repository Structure

```
skills/
└── okf-open-knowledge-format/
    ├── SKILL.md              # Main skill documentation
    ├── scripts/
    │   └── validate.sh       # OKF v0.2 bundle validator
    └── references/
        ├── spec-v02.md       # OKF v0.2 specification
        ├── spec-v01.md       # OKF v0.1 specification (legacy)
        ├── conversion.md     # Conversion guides (Notion, Obsidian, CSV)
        └── examples.md       # Example bundles with v0.2 features
```

## Fork Notice

This repository was forked from [fabricioctelles/skills](https://github.com/fabricioctelles/skills) by [ft.ia.br](https://ft.ia.br). Other skills from the original collection have been removed; this fork focuses exclusively on enhancing and improving the OKF skill.

## License

Apache 2.0 — see [LICENSE](LICENSE) for details.

## References

- [OKF Specification v0.2](https://github.com/GoogleCloudPlatform/open-knowledge-format/blob/main/okf/SPEC.md) — The upstream spec by Google Cloud
- [Open Knowledge Format](https://github.com/GoogleCloudPlatform/open-knowledge-format) — Google's reference implementation and examples
- [Karpathy's LLM Wiki Gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — The pattern OKF formalizes
- [okflint](https://github.com/mattdav/okflint) — Dedicated Python linter for OKF bundles
- [Agent Skills](https://agentskills.io) — The skill format specification
