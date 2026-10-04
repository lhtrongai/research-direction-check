# Evaluation protocol

## Conditions
Each case is run under three conditions, with the same model and effort within a model:
1. **No skill:** the agent receives only the plan and is asked to review it.
2. **Baseline skill:** `review-research-plan` from reed-yang/research-utils, unmodified, linked not copied.
3. **This skill.**

## Isolation rules (learned the hard way during the pilot)
- One fresh session per run. No memory, no connectors (mail, drive, docs), no earlier reviews of the plan.
- Each condition gets its own workspace containing only the plan and, if any, its own skill. Never ship both skills in one archive.
- Prompts must not be ambiguous. "No information beyond the plan" was once read as "do not search the web".
- On Windows PowerShell 5.1, avoid double quotes inside prompts passed as arguments.
- Output files from one run must never be committed where another run can read them.

## Cases built from public papers (learned in smoke tests, October 2026)
- A plan written from a public paper is almost always found by Step 1, even when the paper has no arXiv version: rejected submissions are often published later at another venue, and search engines index OpenReview titles and abstracts. Finding it is correct behaviour, but it lets the skill read the paper's own results.
- For such cases, the run prompt states that any paper matching the plan almost exactly is the author's own draft: do not use its content, and continue as if it did not exist. Runs that still use it are graded separately.
- Report cases in tiers: in-sample (cases that shaped the skill), pre-cutoff (reviews published before the model's knowledge cutoff), post-cutoff (reviews published after it). Never pool tiers in one number.

## Rubric
Written **before** any run, from the case's known errors. For held-out cases the errors come from independent reviewers. Each item is scored caught / partial / missed. Partial means the point is made only vaguely, or a blocking error is rated as a minor concern. Item f records whether the run recommended a direction already published.

## Metrics
- Catch rate per item and overall, per condition and model.
- False alarms: findings the grader judges wrong, listed one by one.
- Harmful recommendations (item f).

## Pilot caveats
The pilot used one case that motivated the skill, and the skill was revised after watching runs on it. Its scores are in-sample. Haiku 4.5 in Claude Code had no web search tool, so item b was not measurable there.
