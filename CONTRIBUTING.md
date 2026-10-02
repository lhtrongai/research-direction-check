# Contributing

The skill only gets better from real failures. The most useful contributions are, in order:

1. **A run where the skill missed something or raised a false alarm.** Open an issue with the "Miss or false alarm" template. Include the model, the skill version, the plan (or a public paper) and the output.
2. **An evaluation case.** A research plan or a rejected paper with known errors, plus a rubric written before running anything. See [`eval/cases/README.md`](eval/cases/README.md).
3. **Domain knowledge** for `references/robot-learning.md`: confounds, reporting conventions or reproduction pitfalls that recur in robot learning.
4. **Changes to `SKILL.md`.**

## Rules for changes to the skill

- **Every change needs a case that motivated it.** Link the issue or eval case.
- **Every change must not break other cases.** Run the evaluation cases before and after, and report both in the pull request.
- **Write steps, not facts.** The skill holds procedures ("search the last 18 months for this measurement"), never findings that go stale ("paper X is the closest work").
- **Keep `SKILL.md` under 200 lines.** Long material goes to `references/`.
- **No dependence on the strongest model.** If a step only works on the largest model, the step needs clearer wording.

## Privacy

Do not submit unpublished plans without the owners' consent. Remove names, institutions, project codes and internal links before you submit.

## License

By contributing you agree that your contribution is released under the MIT License of this repository.
