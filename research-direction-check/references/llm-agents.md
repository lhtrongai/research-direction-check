# Language models and agents

Domain checklist for Steps 2 to 4 of `SKILL.md`. Experimental: every check cites a source checked on 2026-10-04, but no held-out evaluation cases exist yet. Last reviewed: 2026-10-04 (review yearly; the principles age slowly, benchmark names in the examples age fast).

Use when the plan trains, adapts or compares language models, or builds or compares LLM agents.

| Check | What the plan must state | Source |
|---|---|---|
| Contamination | How the benchmark could have entered pretraining or fine-tuning data, and a check or a held-out, newer or private test set. | Oren et al., ICLR 2024, "Proving Test Set Contamination in Black Box Language Models" |
| Prompt format | One prompt format for every model, or the spread across several equivalent formats. | Sclar et al., ICLR 2024 (up to 76 accuracy points between equivalent formats; format effects correlate weakly across models, so a fixed arbitrary format is not a fair comparison) |
| Model-graded evaluation | When an LLM is the judge: answer order swapped, length controlled, judge not from the family of a compared model, agreement with human labels on a sample. | Zheng et al., NeurIPS 2023, "Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena" |
| Error bars | Intervals on every score; paired comparison on the same questions; clustered errors when questions share a passage or task. | Miller, 2024, "Adding Error Bars to Evals" (arXiv 2411.00640) |
| Cost-controlled agents | Accuracy reported next to cost (tokens, calls, money), against simple baselines such as retrying or escalating to a stronger model. | Kapoor et al., TMLR 2025, "AI Agents That Matter" (accuracy-only evaluation produced needlessly costly agents and mistaken conclusions about where gains come from) |
| Agent holdout | A holdout set the agent design was never tuned on; shortcuts that exploit the benchmark ruled out. | Kapoor et al., TMLR 2025 (many agent benchmarks have inadequate or no holdout sets) |
| Reproducibility | Model versions and dates, sampling settings, tool versions and the evaluation harness stated. | Kapoor et al., TMLR 2025 (lack of standardization led to pervasive irreproducibility) |
