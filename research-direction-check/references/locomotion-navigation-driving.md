# Locomotion, navigation and driving

Domain checklist for Steps 2 to 4 of `SKILL.md`. Experimental: every check cites a source checked on 2026-10-04, but no held-out evaluation cases exist yet. Last reviewed: 2026-10-04 (review yearly; the principles age slowly, benchmark names in the examples age fast).

Use when the plan studies legged or humanoid locomotion, embodied navigation or driving and planning.

| Check | What the plan must state | Source |
|---|---|---|
| Open or closed loop | Claims about driving or planning behaviour need closed-loop evaluation; open-loop scores against logged trajectories support only prediction claims. Shortcut inputs (for example ego status) need an ablation. | Dauner et al., CoRL 2023, "Parting with Misconceptions about Learning-based Vehicle Motion Planning"; Li et al., CVPR 2024, "Is Ego Status All You Need for Open-Loop End-to-End Autonomous Driving?" |
| Simulation ranking | A ranking claimed for real robots needs real tests or a measured sim-vs-real correlation. | Kadian et al., RA-L 2020, "Sim2Real Predictivity" |
| Navigation measures | Success plus success weighted by path length; a time-based measure for robots with complex dynamics. | Anderson et al., 2018, "On Evaluation of Embodied Navigation Agents"; "Success Weighted by Completion Time" (arXiv 2103.08022) |
| Locomotion test set | Held-out terrain, pushes or payloads, the same for every method. | General principle (Cobbe et al., 2020); no locomotion-specific source yet |
| Sim-to-real design | Domain randomization ranges, system identification and reward terms listed and matched across compared methods; a difference is a confound. | Inference from Ha et al., 2024, "Learning-based legged locomotion; state of the art and future perspectives" (arXiv 2406.01152) |
| Safety | Falls, collisions or other infractions, and torque or speed limits, reported next to success. | Anderson et al., 2018; Kress-Gazit et al., 2024 |
| Real-robot trials | Trials per condition, initial conditions and reset protocol, a statistical test and failure modes. Real-robot samples are often 10 to 50 trials, so intervals matter. Applies to real-arm manipulation as well. | Kress-Gazit et al., 2024, "Robot Learning as an Empirical Science: Best Practices for Policy Evaluation" (arXiv 2409.09491); "Is Your Imitation Learning Policy Better than Mine?", RSS 2025 |
