# OKF Actor Convention

Fields that record identity (`generated.by`, `verified[].by`, `sources[].author`) use a single actor convention:

## Actor Formats

- **`<producer>/<version>`** for agents and tools: `reference_agent/gemini-2.5-pro`
- **`human:<id>`** for a person: `human:sanath`
- **`process:<id>`** for an automated process: `process:finance-nightly`

## Trust Implications

Consumers that classify trust key off the `human:` prefix, so producers MUST use it for hand-authored or human-confirmed content.

## Examples

```yaml
# Agent-generated content
generated: { by: reference_agent/gemini-2.5-pro, at: 2026-06-20T22:53:05Z }

# Human-verified content
verified: { by: human:sanath, at: 2026-06-25T09:00:00Z }

# Process-verified content
verified: { by: process:finance-nightly, at: 2026-06-26T02:00:00Z }

# Source author
sources:
  - id: rev-policy
    resource: https://wiki.acme/finance/revenue-recognition
    title: Revenue recognition policy
    author: team:finance-fpa
```
