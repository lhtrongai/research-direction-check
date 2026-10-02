# Changelog

## 0.4.0 (2026-10-01)
- A plan's own statement that two arms are controlled or matched is treated as a claim to check, never as a source for the confound table.

## 0.3.0 (2026-10-01)
- Step 1 web search runs whenever a search tool exists; "no information beyond the plan" no longer cancels it.
- A pair may be called controlled only when every confound cell is filled from a source and equal.
- Verdict chosen mechanically: any BLOCK gives DO NOT COMMIT YET; if Step 1 did not run, the verdict is INCOMPLETE.

## 0.2.0 (2026-10-01)
- Full report written in the chat first; documents only on request; never end on a partial report.
- Search budget of about 12 queries and 8 papers opened; fallback citation indexes when one rate-limits.
- Missing inputs can be pre-answered ("anything missing counts as not decided").
- Step 0: a plan that does not name its main question gets a BLOCK; the skill never picks one for the user.

## 0.1.0 (2026-09-30)
- First version: gates G1 to G3, Steps 0 to 7, robot learning reference file.
