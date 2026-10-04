# Robot learning checklists

Domain detail for Steps 1 to 5 of `SKILL.md`. This file holds checklists and arithmetic, not facts. Nothing here names a current model, a benchmark result or a venue rule, because those go stale; look them up in the run.

Version 0.1.0, 2026-09-30. Last reviewed: 2026-10-04 (review yearly).

## 1. Prior art: where it hides (Step 1)

Beyond a general web search, look in:

- arXiv listings for robotics, machine learning, vision and language.
- OpenReview pages of robot learning and machine learning venues, including rejected and withdrawn submissions. Their reviews show what was tried and what reviewers objected to.
- Workshop papers of those venues.
- The code repositories of the benchmark and of each model: lists of papers that use them, issues, forks.
- Leaderboards for the benchmark.
- The "cited by" list of each origin paper on a citation index (Semantic Scholar, Google Scholar, OpenAlex).

Rules for reading what you find:

- Match on what is measured, not on names. Benchmarks in this field are extended under near-identical names (new task suites, perturbation sets, language or visual variants, harder versions). An extension of the plan's benchmark counts as the same benchmark for the Step 1 rule.
- "Newer" means released after the plan's model. "Stronger" means reported higher than the plan's model on the same benchmark, on a page you opened. Do not rank models from memory.
- The field moves monthly. Sort results by date and look at the last three months separately. A preprint that already reports the measurement counts for this check whatever the venue's concurrent-work policy says; report that policy from the fetched guidelines next to the finding.

The "how the plan differs" sentence, with placeholders:

- Does not count: "We evaluate more comprehensively than [paper]."
- Counts: "[Paper] varies [property A] and holds [property B] fixed (their Table n). This plan varies [property B]. If B matters, their ranking of models could change."

## 2. Confound axes (Step 2)

Fill every row for every arm. Take values from the plan first (`[USER]`), then from the model's own paper, model card or official repository (`[WEB]`). Never fill from memory. A row that differs between arms, or is unknown for any arm, is a possible confound.

| Group | Record for each arm |
|---|---|
| Observations | number and placement of cameras (third-person, wrist); image resolution; frame history; whether proprioceptive state is used; depth, tactile, force or other sensors |
| Language input | instruction format and prompt template; language encoder or vision-language model |
| Backbone | vision encoder; language or vision-language backbone; parameter count; which parts are frozen |
| Pretraining | robot datasets, their scale and embodiments; web or vision-language pretraining; whether the evaluation benchmark's data, or data from the same simulator or scenes, was seen |
| Action output | representation and head (discrete tokens, regression, diffusion, flow); action space (end-effector delta, absolute, joint); chunk length and actions executed per prediction; control frequency; action normalisation |
| Adaptation | fine-tuned on the benchmark or zero-shot; which demonstrations and how many; training steps; full or parameter-efficient tuning; augmentation; who trained the checkpoint (official release or own run); how the checkpoint was selected |
| Evaluation protocol | tasks and suite version; episodes per task; initial-state set; seeds; maximum steps; success criterion; simulator and renderer version; precision or quantisation at inference; post-processing of actions |
| Real robot | operator; object set and placement procedure; lighting; trial order (arms interleaved or not); hardware state |

When one model is compared with itself across conditions (clean versus perturbed, one setting versus another), the confounds sit in the conditions:

- Does the manipulation change only the intended property? State how that was verified (a rule, a human check of a sample). A manipulation that also changes what the task asks for measures a different task, not the policy's sensitivity.
- Are the same tasks, initial states and seeds used in every condition, so that episodes pair up?
- Is the number of episodes the same in every condition?
- Were the conditions, thresholds and examples fixed before looking at results?
- For generated manipulations: how many were generated, how many were discarded, and by what rule?

Designs that separate a factor from the rest:

| Design | What it supports |
|---|---|
| Controlled pair: same backbone, data, inputs and protocol, only the factor swapped | a causal claim about the factor, for that backbone and data |
| Ablation: remove or mask the extra difference in one arm | removes that one confound. Say whether it was done by retraining or at inference, because a policy trained with an input can fail without it for an unrelated reason |
| Crossed design: several models at each level of the factor, with the other axes not lined up with the factor | an association across models; causal only if the crossing is complete |
| Paired conditions within one checkpoint: same initial states and seeds, only the condition changes | a causal claim about the condition's effect on that checkpoint |
| None of these is affordable | descriptive wording only |

Wording:

- Descriptive, always allowed: "On [benchmark], A reached x% and B reached y% under [condition], n episodes each." "The policies we tested differ in [list]; we do not attribute the gap to any single component."
- Needs one of the designs above: "because of", "due to", "is caused by", "[component] makes policies more robust", "[architecture class] is better at".

## 3. Samples: what they can detect (Step 3)

What counts as a sample:

- An episode is a sample only if something random differs between episodes: the initial state, the scene, or the policy's own sampling. Rerunning a deterministic policy from the same initial state largely repeats the outcome and adds little. Count distinct initial states.
- Episodes are nested in tasks. For a fixed task list, the pooled success rate over all episodes can use the table below (it is conservative). For a claim about tasks in general, the tasks are the sample and n is the number of tasks.
- One trained or fine-tuned checkpoint is one draw from the training procedure. A gap between two checkpoints may be training-seed noise. A claim about a method or an architecture needs several training seeds per arm or several models per level; otherwise word it as a claim about those checkpoints.
- When a plan says "seeds", find out whether they are training seeds or evaluation seeds. Evaluation seeds add episodes. They do not add training runs.

Lookup table for binary success rates. All values are percentage points.

| Episodes per arm | 95% interval half-width, success near 50% | Half-width, success near 90% | Smallest detectable difference, baseline near 50% | Smallest detectable difference, baseline near 90% |
|---|---|---|---|---|
| 10 | ±26 | ±19 | about 50 | about 60 |
| 20 | ±20 | ±14 | about 40 | about 40 |
| 50 | ±13 | ±9 | 27 | 23 |
| 100 | ±10 | ±6 | 19 | 15 |
| 200 | ±7 | ±4 | 14 | 10 |
| 500 | ±4 | ±3 | 9 | 6 |
| 1000 | ±3 | ±2 | 6 | 4 |

Half-widths are half the width of a Wilson interval. Detectable differences assume two independent arms with equal episodes, a two-sided test at 5% and 80% power; the 90% column is for detecting a drop. Rule of thumb: the detectable difference is two to two and a half times the half-width. Between rows, compute: half-width ≈ 1.96 × sqrt(p(1−p)/n); detectable difference ≈ 2.8 × sqrt(2p(1−p)/n), with p the average of the two success rates.

How to use it:

- Reading a gap between two arms: below about 1.4 times the half-width it is within noise. Do not build a conclusion on it.
- Sizing: pick the row whose detectable difference is at or below the difference the conclusion needs. That row is the sample the claim requires.
- Paired runs (both arms on identical initial states) detect smaller differences. Analyse them with McNemar's test on the pairs where the arms disagree, and size them from the disagreement rate in a pilot.
- Near 0% or 100% there is no room for a gap. A conclusion about improvement on a saturated suite needs a harder condition.
- Several conditions times several models means many tests. Mark one contrast as the main one in advance and label the rest exploratory, or correct for multiplicity.
- Report per-task results. A pooled gain that comes from one or two tasks does not support "across tasks".
- On real robots, 10 to 50 trials per arm detect only very large gaps (top rows). Sequential testing reaches a decision in fewer trials; see section 7.

Cost arithmetic: episodes = arms × conditions × tasks × episodes per task × evaluation seeds. Hours = episodes × seconds per episode ÷ 3600 ÷ parallel environments, plus reruns at the failure rate seen in the pilot. Cost training and fine-tuning runs separately. Seconds per episode comes from the user's own timing; without it, the first job is a timing pilot on one task.

## 4. Reference point: matching checklist (Step 4)

Reproduce first: each model checkpoint on the unmodified benchmark under the published protocol, before any new condition. Then fill the side-by-side table (omit the closest-paper column if Step 1 kept no paper):

| Model checkpoint | Published (source, n) | Closest paper (source, n) | Own run (n, interval) | Gap | Explanation |
|---|---|---|---|---|---|

Conditions to match. Each one can move the number by itself:

- Checkpoint identity: exact name, revision or hash, and where it was downloaded.
- Benchmark: suite, task list, version, initial-state files.
- Simulator and renderer version, physics settings.
- Observations: cameras used, image resolution, preprocessing.
- Action execution: chunk length, actions executed per prediction, control mode and frequency, normalisation statistics.
- Episode protocol: episodes per task, seeds, maximum steps, success criterion.
- Inference: numeric precision or quantisation, sampling settings, library versions.
- Anything the original authors changed from the benchmark default.

Acceptance: the gap between the own number and the published one is within noise by the reading rule in section 3. If it is larger, find the cause before running new conditions; an unexplained gap makes every later number uninterpretable.

Anchor to the closest paper: where the plan overlaps a kept paper (same model, same condition), rerun at least one of its cells. Agreement shows the two pipelines measure the same thing. Disagreement is a finding to explain.

No published number for the exact checkpoint and benchmark (for example a checkpoint the user fine-tuned): use the nearest published setup, list what differs, and say that the reference is indirect.

## 5. Scope axes (Step 5)

Fill for each conclusion:

- Checkpoints: which, how many, official or own.
- Model family or architecture class represented, and by how many members.
- Adaptation regime: fine-tuned on the benchmark's demonstrations or zero-shot.
- Pretraining data.
- Benchmark: suites, tasks, task types (pick and place, articulated objects, long horizon, contact-rich).
- Simulation or real; if simulation, which simulator.
- Embodiment: robot, gripper or hand, control mode.
- Conditions tested: the set of perturbations, languages, scenes or objects.
- Metric: binary success, progress score, time.

Reading rules:

- One checkpoint supports a claim about that checkpoint. Raise at least MINOR "single model" even when the wording is already narrow, with two options: add a model from a different family, or keep every claim tied to that checkpoint.
- A claim about a class (an architecture, a training recipe, a model family) needs several members that differ from each other on the other axes of section 2.
- Simulation results support claims about that simulator and suite. A claim about real robots needs real-robot results or an explicit argument for transfer. Read what the fetched reviewer form says about simulation-only evidence.
- A mean over tasks supports "on average over these tasks", not "on every task".
- A finding under one set of conditions (one perturbation set, one language, one scene distribution) does not extend to conditions that were not tested.

## 6. Worked example (invented plan)

Conclusion C1 in the plan: "Tactile sensing improves insertion success." Comparison: a vision-plus-tactile policy against a vision-only policy.

| Comparison | Factor under study | Arms (n) | Other differences | Wording allowed |
|---|---|---|---|---|
| tactile policy vs vision-only policy | tactile input | 2 | tactile policy trained on twice the demonstrations `[USER, plan section 3]`; runs at a higher control frequency `[USER, config]`; backbone of the vision-only arm unknown | descriptive only |

Finding: BLOCK, Step 2. C1 attributes the gap to the sensor while the demonstrations, the control frequency and possibly the backbone also differ. Basis `[USER]`. Evidence that clears it, any one of: retrain the vision-only arm on the same demonstrations at the same frequency; retrain the tactile policy without its tactile input and compare; rewrite C1 as "policy A succeeded more often than policy B on these tasks" and drop the attribution.

## 7. Standards to fetch

Open these in the run; do not quote them from memory. Also search for newer work that supersedes them.

- Snyder et al., 2026, "Beyond Binary Success: Sample-Efficient and Statistically Rigorous Robot Policy Comparison", arXiv:2603.13616. Sequential, statistically rigorous comparison of two policies, including metrics finer than binary success.
- "Robot Learning as an Empirical Science: Best Practices for Policy Evaluation", 2024, arXiv:2409.09491. Evaluation and reporting practice.
- The reviewer form of the target venue, fetched as described under "Report" in `SKILL.md`.
