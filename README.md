# Research Direction Check

**A pre-commit review for robot learning research plans.** Run it before you commit to a topic, after your first results, and before you write the introduction. It asks the questions reviewers ask under *novelty* and *soundness*, while the plan is still cheap to change.

Built as an [Agent Skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) (`SKILL.md` plus one reference file). It runs in Claude (claude.ai, Claude Code) and was also tested with OpenAI Codex, which reads the same files as plain instructions.

> Status: **v0.5.0, early release** (versions 0.1 to 0.3 were internal iterations; see the changelog). Version 1.0 will follow the held-out evaluation. The skill is usable now. The evaluation so far is a pilot on one in-sample case (see [Evaluation](#evaluation)); held-out results will be added as they come in.

## Why this exists

It was built after a student research plan had to change direction twice in one month, each time for a reason a reviewer would have raised on day one:

1. **The measurement was already published.** Prior art was not searched deeply enough before committing, and newer papers had run the same measurement on stronger models.
2. **The comparison could not support the conclusion.** Three policies were compared to draw a causal conclusion about their action heads, but the policies also differed in inputs, backbone and training, and there was one checkpoint per architecture.

These are the two most common reasons papers are rejected, at any scale of research. Nothing forces a researcher to answer them before the work starts. This skill does.

## What it checks

| Step | Question | Typical blocker |
|---|---|---|
| 0 | Is there one main question? | Several questions with different factors and outcomes, none marked as main |
| 1 | Has this been measured already? | A paper reports the same measurement on the same benchmark with the same or newer models |
| 2 | Do the arms differ only in the factor under study? | Policies differ in sensors, backbone, pretraining or action execution, so only descriptive wording is allowed |
| 3 | Can the planned sample detect the difference the claim needs, within budget? | The main claim needs a smaller difference than its sample can detect |
| 4 | Has the pipeline reproduced a published number? | No reference table against the closest paper |
| 5 | What does each conclusion actually cover? | Claims about "VLA models" from three checkpoints in one simulator |
| 6 | Does the title promise what the design can deliver? | "Cross-architecture study" without a controlled architecture comparison |
| 7 | One page for a human expert | (always produced) |

Every finding is BLOCK, MAJOR or MINOR, cites its basis (`[USER]` plan, `[WEB]` source, or `[INFER]`), and every blocker states the evidence that would clear it. The verdict is mechanical: any BLOCK gives **DO NOT COMMIT YET**; if prior art could not be searched, the verdict is **INCOMPLETE**.

## What it is not

- **Not a substitute for a human reviewer.** Step 7 exists so you send a one-page summary to someone in the field.
- **Not a paper reviewer.** It runs before the paper exists.
- **Not a judge of taste.** It does not rate how exciting an idea is.

## Install

- **claude.ai:** download the `.skill` file from the latest release and upload it as a skill.
- **Claude Code:** copy the `research-direction-check/` folder into `~/.claude/skills/` (or `.claude/skills/` in a project).
- **Other agents (e.g. Codex):** give the agent the folder and ask it to follow `SKILL.md`.

## Use it well

- **Independence is labelled, not required.** The skill runs in any session and rates it Independent, Context (memory about you or the plan) or Co-author (this chat helped write the plan). Facts from memory are tagged and never count as evidence. For a final go or no-go decision, run it once in a fresh session with only the skill and the plan.
- **A model with web search.** Step 1 is the most valuable step and needs search. In our tests, Claude Haiku 4.5 in Claude Code had no search tool, so prior art could not be checked there.
- **Treat findings as things to verify.** Open the cited papers before acting on them.
- **Optional local profile.** Put your budget, target venue and deadline in `research-profile.local.md` (git-ignored) so the skill does not ask every time.

## Evaluation

### Pilot (in-sample, v0.2 to v0.4)

One real student plan (not released) was reviewed under three conditions: no skill, a general-purpose plan-review skill ([review-research-plan](https://github.com/reed-yang/research-utils/tree/master/review-research-plan), used unmodified as a baseline), and this skill. A rubric of five known errors was written **before** the runs, plus one harmful outcome:

- a. confounded comparison between policies
- b. prior art that already covers the claimed gap
- c. causal claim from too few models
- d. title promising more than the design supports
- e. several questions with no main question
- f. *(harmful)* recommending a direction that has already been published

Score out of 5 (half point = partially caught); "f" marks runs that made the harmful recommendation.

| Model | No skill | review-research-plan | This skill |
|---|---|---|---|
| Claude Opus 5.5 (Claude Code) | 5 | 4.5 | 5 (v0.2) |
| Claude Sonnet 5.5 (Claude Code) | 4.5, f | 4.5 | 5 (v0.2) |
| Claude Haiku 4.5 (Claude Code, no web search) | 0.5, f | 0.5, f | 3 (v0.2) / 2.5 (v0.3) |
| GPT-6.1 Sol (Codex CLI) | 3.5 | 4 | 5 (v0.3) |
| GPT-6 Luna (Codex CLI) | 3.5 | 4, f | 5 (v0.3) |

**Read these numbers with care.** This case motivated the skill, and three fixes (v0.2 to v0.4) were made after watching runs on it, so the skill's scores are in-sample. The most robust observation is about the harmful outcome: without a skill, or with a general plan-review skill, weaker models sometimes recommended a research direction that a 2026 paper had already covered. This skill did not do so in any run. Strong models without any skill already caught most errors.

Full protocol and caveats: [`eval/README.md`](eval/README.md).

### Held-out evaluation (planned)

- Real research plans from other students, labelled blind by their supervisors' feedback.
- Rejected robot learning submissions on OpenReview whose reviews were published after the models' knowledge cutoff (ICLR 2027), cut to abstract and method, with titles paraphrased so the agent cannot find its own reviews.
- Reported as catch rate and false-alarm rate per condition and model.

## Related work

| Skill | Difference |
|---|---|
| [reed-yang/research-utils `review-research-plan`](https://github.com/reed-yang/research-utils) | General research plans, any field. No confound table, no reproduction step, no evaluation numbers. Used here as a baseline. |
| [claesbackman/AI-research-feedback `review-pap`](https://github.com/claesbackman/AI-research-feedback) | Pre-analysis plans in economics; six subagents. Its scope guard is adapted in this skill's G2 (MIT). |
| [UnaryLab/ai-for-research `idea-evaluate`](https://github.com/UnaryLab/ai-for-research) | Rates the impact of an idea. Use it for taste; use this skill for soundness. |

## Contributing

Misses, false alarms and new evaluation cases are the most useful contributions. See [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Changelog

See [`CHANGELOG.md`](CHANGELOG.md).

## License

MIT, see [`LICENSE`](LICENSE). Author: Trong Hoang Le.
