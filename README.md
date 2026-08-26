<div align="center">

# HiP-LR

### Hierarchical Planning with Localized Failure Recovery for Long-Horizon Multi-Robot Tasks

[![Paper](https://img.shields.io/badge/Paper-EMNLP%202026%20Findings-b31b1b.svg)](#citation)
[![Venue](https://img.shields.io/badge/Venue-EMNLP%202026-blue.svg)](https://2026.emnlp.org/)
[![Code](https://img.shields.io/badge/Code-Coming%20Soon-lightgrey.svg)](#release-plan)
[![Simulator](https://img.shields.io/badge/Simulator-OmniGibson%20%2F%20BEHAVIOR--1K-orange.svg)](https://behavior.stanford.edu/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

**Authors** · <!-- 저자 목록 -->
<!-- 소속 -->

[**Paper**](#) · [**Project Page**](#) · [**Video**](#)

</div>

---

> [!NOTE]
> **This paper has been accepted to the Findings of the Association for Computational Linguistics: EMNLP 2026.** 🎉
>
> The code, PTD lookup tables, and benchmark configurations are currently being cleaned up for release and **will be made publicly available in this repository.** Please ⭐ star or watch the repo to be notified.

---

## Overview

LLM-based planners produce symbolic plans that look correct on paper but break down the moment they touch a physical simulator. Actions take an unknown amount of time, skills fail at execution level, and multiple robots contend for the same physical space. We refer to this mismatch as the **grounding gap**.

**HiP-LR** closes this gap by connecting two lines of work that have so far developed independently — *learned grasp/skill grounding* and *multi-robot task allocation and scheduling*. Scene-graph-conditioned predictions of **action duration** and **failure probability** are fed directly into a closed-loop scheduler, so that coordination decisions are made *proactively* rather than repaired after the fact. When a failure does occur, recovery is **localized**: it is contained at the skill level instead of triggering a full replan of the task hierarchy.

<div align="center">
  <img src="assets/framework.png" width="90%" alt="HiP-LR framework overview">
  <br>
  <em>Figure 1. Overview of the HiP-LR framework.</em>
</div>

## Key Ideas

- **Grounded duration & failure modeling.** Action outcomes are modeled with **phase-type distributions (PTD)** with dual absorbing states (success / failure), fitted from measured skill-execution data and stratified by congestion and grasp difficulty.
- **Localized failure recovery.** Skill-level failures are detected and resolved at the execution layer, keeping the symbolic plan intact and avoiding cascading replans over long horizons.
- **Allocation–scheduling co-refinement.** Failure probability enters the scheduler as a cost term, and the scheduler assigns explicit start times — not merely an ordering — using probabilistic congestion queries.
- **Long-horizon, heterogeneous, multi-robot.** Evaluated on home-rearrangement tasks with heterogeneous robot teams in realistic simulation.

## Framework

| Module | Name | Role |
| :--- | :--- | :--- |
| **M1** | PTD Modeling | Scene-conditioned duration & failure distribution over skills |
| **M2** | Failure Detection | Execution-layer detection of skill-level failures |
| **M3** | Shared Memory & Recovery | Localized recovery with team-shared execution context |
| **M4** | Allocation–Scheduling Co-Refinement | Risk-aware allocation and start-time scheduling |

## Environment

Experiments are conducted in **OmniGibson / BEHAVIOR-1K**, built on top of the **COHERENT** multi-robot coordination infrastructure, with heterogeneous robot teams performing long-horizon household rearrangement tasks. Baselines are drawn from recent LLM-based multi-robot planners in the same setting.

## Release Plan

- [ ] Core HiP-LR implementation (M1–M4)
- [ ] PTD fitting pipeline & lookup tables
- [ ] OmniGibson / BEHAVIOR-1K task configurations and skill wrappers
- [ ] Benchmark scripts and baseline reproduction
- [ ] Pretrained artifacts and evaluation logs

*Estimated release: <!-- 시점 -->*

## Citation

If you find our work useful, please consider citing:

```bibtex
@inproceedings{hiplr2026,
  title     = {HiP-LR: Hierarchical Planning with Localized Failure Recovery
               for Long-Horizon Multi-Robot Tasks},
  author    = {},
  booktitle = {Findings of the Association for Computational Linguistics: EMNLP 2026},
  year      = {2026}
}
```

## Acknowledgments

This work builds on [BEHAVIOR-1K / OmniGibson](https://behavior.stanford.edu/) and the COHERENT multi-robot coordination framework. We thank the authors of these projects for releasing their code.

## Contact

For questions about the paper or the upcoming code release, please open an issue or contact <!-- 이메일 -->.
