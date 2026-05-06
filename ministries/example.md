---
id: example-ministry
name: Example Ministry
mirrors_real_world: false
---

# Example Ministry

Reference ministry for the worked example. Real deployments map
each ministry 1:1 to a real-world ministerial portfolio (the
Contrast widget depends on this — see
`docs/handoff/02_ARCHITECTURE.md` L2 Shadow State).

## Scope

- Catch-all for Phase 1 demonstration patches
- No real subject-matter focus — that's a deployment-specific decision

## Heads (configured separately)

A real deployment defines a `Head:example-ministry` agent under
`agents/heads/`. Phase 1 does not require Heads (cabinet vote is
schema-only); add when activating CROSS_CUTTING / CONSTITUTIONAL
pipelines.
