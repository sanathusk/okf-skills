# OKF Attested Computation Rules

An Attested Computation concept carries not just what a value *means* but a sanctioned way to *compute* it, so a consumer can confirm the agent ran the blessed computation instead of improvising its own.

## When to Use

- Financial metrics where compliance requires audit trails
- KPIs that must be computed consistently across reports
- Any calculation where "did the sanctioned thing run" matters

## Concept Structure

A sanctioned computation is a standalone concept of `type: Attested Computation`. A concept that needs the value links to it with a normal markdown link.

## Required Fields

| Field | Description |
|-------|-------------|
| `runtime` | REQUIRED. How to run it: `bigquery`, `postgres`, `dbt`, `python`, `Looker` |
| `parameters` | List of `{ name, type, required }` — Typed holes the agent fills |
| `computation` | Path to computation file (if not inline in body) |
| `executor` | `{ resource, receipt: [...] }` — How to run and what evidence to capture |
| `attester` | `{ resource }` — Deterministic code that verifies the receipt |

## Computation Delivery

Provide the computation in one of two ways:

1. **Inline:** a single fenced code block in the body under `# Computation`. Best for a short computation reviewed alongside the contract.
2. **File:** set `computation` to a path and omit the body fence. Best for a long or generated computation.

## Agent Rules

1. **Agent fills parameters only** — The agent supplies *values* for declared `parameters`, never edits the computation itself.
2. **Executor produces receipt** — Evidence the attester inspects.
3. **Attester is deterministic** — No LLM, just code that verifies the receipt.

## Example

```markdown
---
type: Attested Computation
title: Revenue for fiscal year
description: Recognized revenue for a fiscal year, per Finance's definition.
status: stable
runtime: bigquery
parameters:
  - { name: year, type: integer, required: true }
executor:
  resource: references/skills/run-on-bq.md
  receipt: [job_id, executed_sql, result]
attester:
  resource: references/attesters/revenue.py
generated: { by: reference_agent/gemini-2.5-pro, at: 2026-06-20T22:53:05Z }
verified: { by: human:sanath, at: 2026-06-25T09:00:00Z }
stale_after: 2026-09-23T00:00:00Z
sources:
  - id: rev-policy
    resource: https://wiki.acme/finance/revenue-recognition
    title: Revenue recognition policy
---

# Computation

    SELECT SUM(amount) AS revenue
    FROM finance.recognized_revenue
    WHERE fiscal_year = @year

The computation binds only the declared `parameters`, per the recognition policy.[^rev-policy]

[^rev-policy]: Revenue recognition policy
```

## Concepts That Use a Computation

A document is rarely a single computation. An income-statement overview that discusses revenue, profit, and margin stays one readable concept and links to one Attested Computation per figure:

```markdown
---
type: Metric
title: Revenue
description: Recognized revenue for a fiscal year.
tags: [finance, revenue]
status: stable
generated: { by: reference_agent/gemini-2.5-pro, at: 2026-06-20T22:53:05Z }
---

# Definition

Recognized revenue sums `amount` over rows booked to the fiscal year,
computed by [the revenue computation](../computations/revenue.md).
```
