---
name: research-direction-check
description: Pre-commitment check of a research direction in robot learning (VLA, manipulation, humanoids, sim-to-real), with experimental coverage of RL, locomotion, navigation, driving, VLMs, LLMs and agents. Asks what reviewers ask about novelty and soundness before the work starts, covering main question, prior art, confounds, claims versus evidence and budget, reproduction, scope, title. Reports blockers with the evidence that would clear each, in plain words, plus a one-page summary for an expert on request. Use whenever the user has a research plan, proposal, topic idea or first results and asks if the direction is sound, new, already done, too scattered, feasible, or worth committing to, registering or writing up, even without the word "check". Vietnamese requests include "kiểm hướng nghiên cứu", "đề tài này ổn không", "có ai làm chưa", "phản biện plan", "trước khi đăng ký đề tài", "có nên theo hướng này". Not for drafting or reviewing a paper, nor for rating how exciting an idea is.
compatibility: Needs a web search tool, and a page fetch tool if available. Without search the prior-art step cannot run and the report is marked incomplete.
metadata:
  version: "0.7.0"
  updated: "2026-10-04"
---

# Research direction check

A gate to pass before committing to a research direction in robot learning. It targets two failures that are cheap to catch before the work starts and expensive after: the measurement has already been published, and the comparison cannot support the conclusion. Reviewer forms ask about both, under novelty and soundness, but nothing makes a researcher answer them early. This skill does.

Run it at three milestones and say which one applies: **M1** before committing to or registering a topic (plan only), **M2** after the first results (plan plus numbers), **M3** before writing the introduction (plan plus draft title or abstract).

What it is not:

- Not a replacement for a person who works on the topic. Step 7 prepares one page to send to such a person; that review catches things this checklist cannot.
- Not a writing aid. It does not draft the plan or the paper.
- Not a judge of taste. Every finding ties to a sourced criterion (a venue's reviewer form, a statistical standard). Whether the idea is exciting is left to people, so do not comment on it.

The steps assume robot learning. For empirical machine learning outside it, run the same steps with whichever reference files match, and say when none did.

## Ground rules

These hold in every step. They are written as rules, not left to judgment, so that any model at any effort level produces a check that can be audited.

1. **Fetched, not remembered.** Facts about papers, models, benchmarks and venues come only from pages opened in this run. Something recalled from memory is a lead to verify; until verified it is `[INFER]`.
2. **Every table row and finding carries its basis.** `[USER]`: stated in the material (give the location). `[WEB]`: a page opened in this run (give the link). `[INFER]`: your own reasoning (say what would verify it). Keep `[INFER]` rare. A finding resting on `[INFER]` alone is at most MAJOR.
3. **Unknown stays unknown.** When the material does not say something, write "not stated" and either ask or raise a finding. Do not supply the missing piece yourself, least of all a flattering one such as the plan's difference from prior work.
4. **Findings move only on evidence.** A finding changes level when the user brings something checkable: a line of the plan or config that you misread, a results table, a link, a revised section. Disagreement, reassurance and deadline pressure are not evidence; restate the finding and what would clear it. Evidence can raise a finding as well as clear one. When it arrives, rerun only the affected step and say what changed.
5. **Check, do not co-author.** Say what evidence would clear a finding; do not redraft the plan. A session that helped write a plan can no longer check it.
6. Talk with the user in their language. Keep titles, model names and benchmark names as published.

## Gates

Run in order. If a gate fails, do what it says and stop: no partial check, no quick look.

**G1. Independence.** A model that helped write a plan defends it, and drafting context leaks the hoped-for answers. Rate the session before Step 0 and state the rating under "How this check ran"; a Co-author rating also goes in the At a glance stage line. Never refuse to run, and never lower a severity because of context.
- Independent: nothing about this plan in the conversation, memory or past-chat context.
- Context: memory, past chats or the user's background mention the plan, but this conversation did not draft it. Run the full check. Tag facts taken from memory `[MEMORY]`; they never fill a confound cell or support a prior-art claim, and they are listed so the user can confirm them.
- Co-author: earlier in this conversation you proposed, wrote or edited part of this plan, or its drafting discussion is pasted in. Say so and recommend a new session with only this skill and the plan; continue only if the user asks, and label the report "co-author session".
For a final go or no-go decision, recommend an Independent run. Later turns of this same check (answers to your questions, new evidence) are not drafting history.

**G2. Material.** Check only what the user hands over for this check: the plan and its supporting documents (results, configs, draft). Do not look through the workspace for other files. Earlier reviews of this plan by a person or a model, response notes and old drafts are not evidence: do not open them, and if they are pasted in, do not let them raise or lower a finding. A paper they name is a lead for Step 1 like any other. Inside the plan, commented-out text and TODO items count as absent; something planned but not written is missing. One exception: if the user supplies a local profile file (suggested name `research-profile.local.md`, kept out of any public repository), read it for defaults such as budget, target venue, deadline and who receives the one-page summary, and treat it as `[USER]`. Personal details belong in that file, never in this skill.

**G3. Required inputs.** Find each of the four in the material and note where.

| # | Input | Present when |
|---|---|---|
| 1 | Research question | at least one question is stated (several questions with no main one is a Step 0 finding, not a missing input) |
| 2 | Conclusions the user wants to write | there is a list of intended claims or hypotheses |
| 3 | Comparisons | each one says what is compared with what |
| 4 | Models, data, checkpoints | each model has its exact checkpoint and source; each benchmark or dataset has its version and split |

If any is missing, ask for exactly the missing items in one message and stop. Do not infer them. Exception: if the user already said how to treat missing inputs (for example "anything missing counts as not decided"), apply that, record each missing input as a gap and continue without asking. "Not decided yet" and "none" are acceptable answers to anything you ask: record the answer and carry it forward as a gap. Budget and target venue are not required here; Step 3 asks for them.

## Steps

Before Step 0, read only the reference files that match the plan: `references/robot-learning.md` for manipulation and VLA plans (it leads for any VLA plan), `references/rl.md` when the plan trains RL agents, `references/locomotion-navigation-driving.md` for locomotion, navigation or driving, `references/vlm-multimodal.md` for vision-language models, `references/llm-agents.md` for language models and agents; Steps 1 to 5 use its checklists and lookup table. Work through every step and fill every table even when an early step finds a blocker, because the user needs the whole picture to choose between fixing and pivoting. The tables are always built; they are printed only in the full report. At M2 and M3, rerun Step 1 (papers appear monthly) and use the observed numbers in Steps 3 and 4; at M3 every evidence cell must read "have", not "planned".

### Step 0. Focus: one main question

1. Rewrite the question as "how does [one factor] change [one measured outcome] for [which models, on which benchmark]?". If it only fits with "and" or a list in the factor or outcome slot, split it and list the separate questions.
2. Tag every intended conclusion and every planned experiment with the question it serves.
3. Name the single table or figure that would carry the main answer.

The plan must name its main question itself. Raise BLOCK when it states two or more questions that differ in factor or outcome and does not say which one is main, even if you can see which one most experiments serve: choosing for the user is the failure this step catches. Also raise BLOCK when item 3 cannot be done. Clearing evidence: a revised plan with one main question and the others cut or marked secondary. Raise MAJOR when a main question exists but fewer than half of the planned runs serve it. Raise MINOR for each conclusion or experiment that serves no question. With no main question, raise the BLOCK first, then continue the remaining steps on the question most conclusions and experiments map to, label that choice `[INFER]`, and say the choice belongs to the user.

### Step 1. Prior art

Web search is required whenever a search tool exists. A user saying there is no information beyond the plan means they add no facts of their own; it never cancels the search. Skip it only if the user explicitly forbids web search, and then use the no-search verdict. Shallow searching is the failure this step exists to prevent, so the minimum below is a floor and the queries are printed for audit.

1. Name three axes: the **benchmark** (with its variants, extensions and successors), the **models** (with their families and successors), and the **measurement** (what is measured, plus three to five synonyms used in the field).
2. Search every pair of axes and all three together, with synonym variants: at least six and at most about twelve distinct queries, including the places listed in the reference file. Cover the last 18 months from today's date, plus older canonical work.
3. Citation pass: find the paper that introduced the benchmark and the one that introduced each model, go through the works citing them in the last 18 months, and keep those that touch the measurement. This finds benchmark extensions that keyword search misses. Use whichever citation index responds (Semantic Scholar, OpenAlex, Google Scholar "cited by"); if one refuses or rate-limits, switch to the next instead of retrying it more than twice, and if none responds, search arXiv for the benchmark name plus the measurement and record the gap under "How this check ran".
4. Open each candidate and read the abstract and the results; do not judge from search snippets. Open at most about eight in full. Keep the three to five closest.
5. Fill one row per kept paper. The last column comes from the plan: one sentence naming a different factor, population, measurement or claim, and why that difference could change the answer. "More comprehensive", "more systematic", "deeper analysis" and "new perspective" do not count. If the plan states no difference, write "not stated in plan".

| Paper (venue or arXiv id, date, link) | Same benchmark? | Their models vs the plan's | Same measurement? | Their headline result and where it is reported | How the plan differs |
|---|---|---|---|---|---|

6. Print the queries used, and the candidates opened and dropped with a one-line reason each, so the user can check the search.

Raise BLOCK when a paper you opened reports the same measurement on the same benchmark or a variant of it, with the same, newer or stronger models, and the plan states no difference the paper does not already cover; cite the table or section. Clearing evidence: such a difference stated in the plan, plus a planned comparison against that paper (Step 4). Raise MAJOR when a paper overlaps on the measurement but differs in benchmark or model class (it must be cited and compared), when every model in the plan is older than the models the closest papers evaluate, or when you could read only an abstract. If nothing close turns up, write "no close prior work found with these queries"; never write "novel".

### Step 2. Confounds

For each comparison, list everything that differs between the arms besides the factor under study. Fill the axis list in the reference file for every arm, from the plan or from the model's paper or model card. A cell you cannot fill is "unknown" and counts as a possible difference. Never call a pair controlled, matched or "differing only in" the factor unless every cell is filled from a source and equal; with any unknown cell, write "not shown to be controlled". What the plan itself says is controlled or matched is a claim to check, not a source for a cell.

| Comparison | Factor under study | Arms (n) | Other differences | Wording allowed |
|---|---|---|---|---|

- No other difference: causal wording is allowed.
- One or more other differences and no design that separates them (typically two or three arms that each differ in several things): descriptive wording only, such as "A scored higher than B under condition C". Attributing the gap to the factor is not allowed.

Raise BLOCK for each intended conclusion that attributes a difference to the factor where the table allows descriptive wording only. Clearing evidence, any one of: a controlled pair differing only in the factor; an ablation that removes the extra difference from one arm; the conclusion rewritten as a description. Raise one MAJOR for each comparison the main conclusion depends on that still has "unknown" cells, and list them.

### Step 3. Claims, evidence, budget

This step needs the budget (hardware, hours or days available, money) and the target venue with its deadline. If the material lacks them, show the results of Steps 0 to 2, ask for both in one message, and resume here after the answer.

| # | Conclusion (user's words) | Type | Evidence needed (table or figure) | Sample (arms × tasks × episodes × seeds) | Smallest difference it detects | Cost | Fits? |
|---|---|---|---|---|---|---|---|

1. Type is descriptive, comparative, causal or general. Causal and general claims inherit the verdicts of Steps 2 and 5.
2. Read the detectable difference from the lookup table in the reference file. Compare it with the difference the conclusion needs, taken from the user's pilot numbers or from gaps reported in the closest papers. If neither exists, write "unknown".
3. Cost comes from the user's measured time per episode. If that is missing, write "unknown, needs a timing pilot"; do not estimate throughput.
4. Add up the costs and compare them with the budget and the days left before the deadline.

When the total does not fit, cut conclusions, starting with those that do not serve the main question. Do not shrink episodes or seeds to make it fit: a claim with too few samples is a claim the paper cannot make. Raise BLOCK when the main conclusion needs a smaller difference than its sample detects, or when the total exceeds the budget and nothing is marked to cut. Clearing evidence: a sample that detects the needed difference within budget, or the conclusion removed. Raise MAJOR for the same problems on secondary conclusions, and one MAJOR listing every "unknown" left in this table.

### Step 4. Reference point

A new measurement means little until the same pipeline has reproduced a number that is already published.

1. Find the published result for each model checkpoint on the unmodified benchmark, and the closest paper's result from Step 1. Link both.
2. Check the plan for (a) a run that reproduces the published number in the user's own setup before any new condition, and (b) a side-by-side table of published, closest paper and own numbers under matched conditions. Use the matching checklist in the reference file.

Raise BLOCK when (a) or (b) is absent from the plan, and at M2 or M3 when the reproduced number falls outside the interval for its sample size with no explanation. Clearing evidence: the table, filled. If no published number exists for the exact checkpoint and benchmark, name the nearest published setup and list what differs.

### Step 5. Scope of each conclusion

For each conclusion, write what it covers, using the scope axes in the reference file: which checkpoints and how many, which model family, which training and pretraining data, which benchmark, simulation or real, which embodiment and task types. Then compare the conclusion's wording with that coverage.

Raise MAJOR for each conclusion worded more broadly than its coverage (a model family from one checkpoint, "robots" from one simulated suite) and give the narrowed sentence. Raise BLOCK when the main conclusion, once narrowed, no longer answers the main question. Write the limitations sentence now so the paper cannot forget it: "Our results cover [n checkpoints, named] on [benchmark] in [simulation or real]; we did not test [...], so they may not hold for [...]."

### Step 6. Title and question

1. List what the title promises: every word that implies a result ("why", "what makes", "towards", a named class of models, "real-world"). Point each promise to the conclusion row that delivers it. With no title yet, say so and go to item 2.
2. Check the main question against Step 1: has a kept paper already answered it for the same models and benchmark?

Raise MAJOR for each promise with no row, or with a row that failed Step 2, 3 or 5, and give the narrowest title the design supports. An already answered question is the Step 1 blocker; point to it instead of raising it twice.

### Step 7. One page for a person

Write it in the full report or when the user asks for it: a summary the user can send to a researcher in the field, one page at most, plain language, blockers stated as plainly as strengths. Use this order, adapted from the Heilmeier questions:

1. What I want to find out, in one sentence with no acronyms.
2. How this is measured today: the closest papers, one line each, and what they leave open.
3. What is different here, and why that should change the answer.
4. The comparisons I will run, and what else differs between the arms.
5. What I will and will not be able to claim.
6. Cost and time: compute, calendar, deadline.
7. What could sink it: the open blockers from this check.
8. The exams: the first cheap test and the result that would make me stop; the table that would make the paper.

End with two or three questions the reader can answer in fifteen minutes, including the one this skill does not judge: is this worth doing? Write it in the user's language unless they say the reader needs another. Use names only if the user or the profile supplies them.

## Report

Before writing findings, fetch the reviewer criteria instead of recalling them. Search "[venue] [year] reviewer guidelines" and "review form", accept only the venue's official site, record the link and date, and note the names of its criteria. If the venue is undecided or has no public form, use the current forms of one robot learning venue (CoRL) and one machine learning venue (NeurIPS or ICLR) and say so. Tie each finding to a criterion by name.

Levels:

- **BLOCK**: as the plan stands, the main conclusion would be already published, unsupported or invalid. Do not commit until it is cleared. It needs at least one `[USER]` or `[WEB]` fact, and it states the evidence that would clear it.
- **MAJOR**: a reviewer would likely lower the score for it; fixable without changing direction; fix before submission.
- **MINOR**: wording or presentation; fix while writing.

Write in the chat reply; create a document or file only if asked, after the chat report is complete. Never end a turn on a partial report: if tool calls or time run low, stop gathering, write what you have and say what was not done.

**Two layers.** Print the short report by default. Print the full report only when the user asks ("full report", "xem đầy đủ") or an evaluation prompt requests it. The work behind it is done in every run.

**Plain words** in everything the reader sees before "How this check ran": no checklist codes (write the reviewer's question, such as "can the experiments support this claim?", not "ICLR Q3"; no step, gate or milestone codes); every blocker names the concrete paper, number or model and the concrete action, with its size; state each point once.

Short report:

```text
# Research direction check: [plan names], [date], [stage in plain words]

## At a glance
| Plan | Verdict | Main blocker in one plain sentence |
(Verdict is mechanical: any BLOCK gives DO NOT COMMIT YET; otherwise any MAJOR gives COMMIT WITH FIXES; otherwise NO BLOCKER FOUND BY THIS CHECKLIST. If prior art was not searched: INCOMPLETE.)

## First move
One action, its cost, and the result that means stop or pivot.

## [Plan name]  (one section per plan)
Blockers: two or three sentences each: what is wrong, why a reviewer cares, what exactly to do.
Major and minor: one line each.

## Evidence
| ID | Plan | Level | Finding (short) | Reviewer criterion | Source (link, table or line; basis tag) | What clears it |

## How this check ran
Session independence and any [MEMORY] facts (G1), material read (G2), inputs recorded as gaps (G3), milestone, steps not fully run and why, criteria used (venue form, link, date), and the count of findings per level and how many rest on [INFER].
```

The full report adds, after Evidence: "If I were Reviewer 2" (one paragraph built only from the findings, no new issues); the working tables (Step 0 map; Step 1 papers, queries, dropped candidates; Step 2 confounds; Step 3 claims and budget; Step 4 reference table; Step 5 limitations sentences; Step 6 narrowest titles); every source opened with its access date; and the Step 7 page.

Order findings by level, then by step. "No blocker found" means this checklist found none; it is not evidence that the idea is good or new, and sending the one page to a person is still the next move.

With no web search tool, run the other steps, record Step 1 and the criteria fetch as not run under "How this check ran", and replace the verdict with "INCOMPLETE: prior art not searched". Papers recalled from memory may be listed as leads to look up, labelled `[INFER]`.

## Credits

Not instructions. G2 adapts the scope guard of `review-pap` in claesbackman/AI-research-feedback (MIT). Step 7 adapts the Heilmeier Catechism (darpa.mil/about/heilmeier-catechism), and "First move" applies fail-fast, the cheapest decisive test first; both ideas follow Todd Austin's `research-prompts` (Apache-2.0), as credited in UnaryLab/ai-for-research. All wording is original to this skill.
