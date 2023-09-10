---
title:  "Exploration & Control"

categories:
  - deepmind_lecture

tags:
  - [Deepmind RL Lecture]

use_math: true
toc: true
toc_sticky: true

date: 2023-09-04
last_modified_at: 2023-09-09
---

In this post, we simplify the seting
- The environment have only single state
  - Actions no longer have long-term consequences in the environment
  - Actions still do impact immediate reward
  - Other observations can be ignored

## Exploration vs. Exploitation
  - Exploitation: Maximise performance based on current knowledge
  - Exploration: Increase knowledge
  - We need to gather information to make the best overall decisions
  - The best long-term strategy may involve short-term sacrifices
  - 
# Formalising the problem
## 🎰 `The Multi-Armed Bandit`
- A multi-armed bandit is a set of distributions $\lbrace \mathcal{R}_a \mid a \in \mathcal{A} \rbrace$
- $\mathcal{A}$ is (known) set of actions (or "arms")
- $ \mathcal{R}$ is distribution on rewards, given action $a$
- The goal is to pick the action, that gives the highest average reward
- At each step $t$ the agent selects an action $A_t \in \mathcal{A}$
- The environment generates a reward $R_t \sim \mathcal{R}_{A_t}$
- The goal is to maximise cumulative reward $\sum^t_{i=1} R_i$
