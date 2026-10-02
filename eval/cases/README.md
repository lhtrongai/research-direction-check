# Evaluation cases

Each case is a folder:

```
eval/cases/<case-id>/
  plan.md      the input the agent sees (plan, or abstract + method of a paper)
  rubric.md    known errors, written before any run, with their source
  source.md    where the case and the errors come from, and dates
```

Rules:
- For papers, keep only the abstract and method, remove results, and paraphrase the title so the agent cannot find its own reviews online.
- The rubric lists each error with what counts as caught, partial and missed.
- A case enters the held-out set only if its errors come from someone other than the skill's authors.
- Runs go in `eval/results/` with model, setting, skill version and date in the file name.
