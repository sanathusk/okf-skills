# OKF Trust Tiers

Consumers derive a trust tier from the `verified` field, lowest to highest:

## Trust Levels

| Condition | Trust Tier |
|-----------|------------|
| No `verified` key | **Unverified** |
| `verified` by non-`human:` actors only | **Machine-confirmed** |
| `verified` by a `human:<id>` actor | **Human-reviewed** |

## Key Rules

- A concept with no trust frontmatter is still consumable; consumers MUST NOT reject it.
- Trust tiers are advisory signals, not access control.
- The `human:` prefix is what determines human-reviewed status.

## Examples

### Unverified (no `verified` key)

```yaml
generated: { by: reference_agent/gemini-2.5-pro, at: 2026-06-20T10:00:00Z }
# No verified key = unverified
```

### Machine-confirmed (non-human verifier)

```yaml
generated: { by: reference_agent/gemini-2.5-pro, at: 2026-06-20T10:00:00Z }
verified: { by: process:schema-validator, at: 2026-06-21T02:00:00Z }
```

### Human-reviewed (human verifier)

```yaml
generated: { by: reference_agent/gemini-2.5-pro, at: 2026-06-20T10:00:00Z }
verified:
  - { by: process:schema-validator, at: 2026-06-21T02:00:00Z }
  - { by: human:domain-expert, at: 2026-06-22T14:00:00Z }
```