# Reinforcement learning: training and comparison

Domain checklist for Steps 2 to 4 of `SKILL.md`. Experimental: every check cites a source checked on 2026-10-04, but no held-out evaluation cases exist yet. Last reviewed: 2026-10-04 (review yearly; the principles age slowly, benchmark names in the examples age fast).

Use when the plan trains RL agents or compares RL algorithms, including RL for robot control. Each row is a confound for Step 2 or a reporting gap for Steps 3 and 4.

| Check | What the plan must state | Source |
|---|---|---|
| Training runs and intervals | Independent training runs per method; interval estimates (stratified bootstrap), robust aggregates (interquartile mean), performance profiles. A ranking claim from point estimates alone is not supported. | Agarwal et al., NeurIPS 2021, "Deep RL at the Edge of the Statistical Precipice" |
| Equal tuning | Tuning protocol and budget for every method, with tuning seeds separate from test seeds. Unequal tuning is a confound. | Eimer, Lindauer, Raileanu, ICML 2023, "Hyperparameters in RL and How To Tune Them" |
| Equal interaction budget | Methods compared at equal environment steps, and at equal wall-clock if speed is claimed. | Patterson, Neumann, White, White, JMLR 2024, "Empirical Design in Reinforcement Learning" |
| Environment and protocol | Exact environment version, termination, frame skip and stochasticity settings (for example sticky actions), matching the numbers cited for comparison. | Machado et al., JAIR 2018, "Revisiting the Arcade Learning Environment" |
| Implementation | A claim about the algorithm needs a shared codebase or an ablation of code-level optimizations. | Engstrom et al., ICLR 2020, "Implementation Matters in Deep Policy Gradients" |
| Offline RL selection | Online evaluations used to choose hyperparameters are counted and reported; results under several budgets. | Kurenkov and Kolesnikov, ICML 2022, "Showing Your Offline RL Work: Online Evaluation Budget Matters" |
| Generalization | Training and test levels or tasks are disjoint. | Cobbe et al., ICML 2020, "Leveraging Procedural Generation to Benchmark RL" |
