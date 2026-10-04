# Vision-language and multimodal models

Domain checklist for Steps 2 to 4 of `SKILL.md`. Experimental: every check cites a source checked on 2026-10-04, but no held-out evaluation cases exist yet. Last reviewed: 2026-10-04 (review yearly; the principles age slowly, benchmark names in the examples age fast).

Use when the plan trains, adapts or compares vision-language models. For a VLA plan, `robot-learning.md` leads; use this file only for claims about the vision-language backbone itself.

| Check | What the plan must state | Source |
|---|---|---|
| Blind baseline | The score of each model with the image removed, per benchmark; items answerable without the image removed or reported separately. | Chen et al., NeurIPS 2024, "Are We on the Right Way for Evaluating Large Vision-Language Models?" (visual content unnecessary for many samples; one model scored 42.7% on MMMU without images) |
| Leakage | Overlap between training data and the benchmark checked, or a leakage measure reported, or benchmarks curated against leakage. | Chen et al., NeurIPS 2024 (unintentional leakage in LLM and LVLM training); Oren et al., ICLR 2024, "Proving Test Set Contamination in Black Box Language Models" |
| Prompt and answer format | One prompt template and one answer-extraction rule for every model, or the spread across formats reported. A fixed, arbitrary format is not a fair comparison. | Sclar et al., ICLR 2024, "Quantifying Language Models' Sensitivity to Spurious Features in Prompt Design" (up to 76 accuracy points between equivalent formats; format effects correlate weakly across models) |
| Hallucination measure | A measure that does not depend on instruction wording and caption length, or robustness to the instruction reported. | Li et al., EMNLP 2023, "Evaluating Object Hallucination in Large Vision-Language Models" (caption-based CHAIR is unstable; polling-based POPE is more stable) |
| Model-graded answers | When an LLM scores open-ended answers: answer order swapped, judge not from the family of a compared model, agreement with human labels on a sample. | Zheng et al., NeurIPS 2023, "Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena" (position, verbosity and self-enhancement biases) |
| Error bars | Intervals on every score; paired comparison on the same items; clustered errors when items share a source. | Miller, 2024, "Adding Error Bars to Evals" (arXiv 2411.00640) |
