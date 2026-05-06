# Canned issue — worked Phase 1 example

This is the input the integration test (Stage 12) uses to drive a
patch end-to-end through the regular pipeline to PUBLISHED. Real
issues come from citizens / operators / `news.ingested` / etc.;
this one is fixed text so the test is reproducible.

Use it manually:

1. Ensure `partyclip-content/constitution/k1-a1.md` is loaded.
2. Ensure the Architect / Critic / Legal / Executor / BiasMirror
   personas in `agents/` are loaded.
3. Ensure `pipelines/regular.yaml` is loaded.
4. POST the issue body below to the runtime's issue intake (Phase 2
   surface; Phase 1 you seed it directly into the database).
5. Watch it advance through the pipeline; sign off at
   `AWAITING_SIGNOFF` via `POST /api/patches/:id/signoff`.

---

## Issue title

Disclose framework cost per published patch on the public site

## Issue body

The framework records cost per patch (`patches.cost_total`,
aggregated from per-stage `PatchStageRun.cost`). Public readers
have no way to see this number today. They should — both for
accountability and to make the framework's resource use legible.

Propose a patch that:

- Mandates that `cost_total` be displayed alongside every published
  patch on the public site, with the same granularity it's stored
  at (no rounding to "free" or "cheap").
- Mandates a per-month aggregate cost figure visible from the
  homepage, broken down by ministry.
- Cites `CONST-K1-A1` as `supporting` (the founding article's
  worked-reference framing).

The patch must not propose to alter operator sign-off, and must not
attempt to amend `CONST-K1-A1` (which is `IMMUTABLE`).

## Expected pipeline outcome

- DRAFTING → CRITIQUE: Architect produces a one-screen draft with
  citations.
- CRITIQUE → RISK_ASSESS: Critic returns PASS (concrete, scoped,
  cited).
- RISK_ASSESS → EXECUTOR: Legal returns PASS (no
  IMMUTABLE_CONFLICT, no UNDERMINES_SIGNOFF).
- EXECUTOR → BIAS_MIRROR: Executor produces a tightened final
  draft preserving the citation.
- BIAS_MIRROR → AWAITING_SIGNOFF: BiasMirror returns PASS or FLAG
  with at most LOW-severity findings.
- AWAITING_SIGNOFF → PUBLISHED: operator signs off with a
  rationale; total elapsed cost is logged and queryable.

If any stage rejects, that's also a valid path through the test —
just ensure the rejection record is structured (no free-text) and
the patch returns to DRAFTING.
