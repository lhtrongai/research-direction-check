# Changelog

## 0.6.0 (2026-10-02)
Found in real use: a check of four plans produced a long, abstract report that opened with internal labels and repeated the same blockers in five sections.
- Two layers: a short report by default (verdict per plan, blockers in plain words, first move, evidence table); the full report (working tables, queries, reviewer paragraph, one-page summary) only on request.
- Plain words before "How this check ran": no checklist, step, gate or milestone codes; every blocker names the concrete paper, number or model and the concrete action.
- One section per plan when several plans are checked; each point stated once.
- Gate results, milestone, criteria and incomplete steps move to a closing section, "How this check ran". Scoring rules are unchanged.

## 0.5.0 (2026-10-02)
- G1 no longer stops the check. It rates the session (Independent, Context, Co-author) and prints the rating. Found in real use: a normal chat with memory refused to check the user's own projects.
- Facts taken from memory are tagged `[MEMORY]`, listed for confirmation, and never fill a confound cell or support a prior-art claim.
- A co-author session still recommends a fresh session and continues only if the user asks.

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
