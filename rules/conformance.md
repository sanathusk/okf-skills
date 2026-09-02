# OKF Conformance Rules

A bundle is **conformant** with OKF v0.2 if:

## The Three Required Rules

1. **Every non-reserved `.md` file** in the tree contains a parseable YAML frontmatter block.
2. **Every frontmatter block** contains a non-empty `type` field.
3. **Every reserved filename** (`index.md`, `log.md`) follows the structure in the reserved files rules when present.

## What Consumers MUST NOT Reject

Consumers MUST NOT reject a bundle because of:

- Missing optional frontmatter fields.
- Unknown `type` values.
- Unknown additional frontmatter keys.
- Broken cross-links.
- Missing `index.md` files.

## Validation Errors

- `E1`: File has no YAML frontmatter
- `E2`: File has frontmatter but no `type` field (or empty)
- `E3`: Reserved file has unexpected structure
- `E4`: Attested Computation missing required `runtime` field

## Validation Warnings (non-blocking)

- `W1`: Missing recommended field `title` or `description`
- `W2`: Broken cross-link
- `W3`: No `generated` field (v0.2 recommended)
- `W4`: No `index.md` in directory
- `W5`: `log.md` dates not in ISO 8601 format
- `W6`: `sources` entry missing `resource` field
- `W7`: `stale_after` date has passed — content is stale