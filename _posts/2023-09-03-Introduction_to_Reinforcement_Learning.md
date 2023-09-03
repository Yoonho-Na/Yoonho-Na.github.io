---
title:  "Introduction to Reinforcement Learning"

categories:
  - deepmind_lecture

tags:
  - [Deepmind RL Lecture]

use_math: true
toc: true
toc_sticky: true

date: 2023-09-03
last_modified_at: 2023-09-03
---

# Notions

## 🧠 `Agent`
At step $t$, the **agent**:
- Receives observation $O_t$ (and reward $R_t$)
- Executes action $A_t$

Agents contains:
- **Agent state**
- **Policy**
- **Value function estimate**
- **Model**

## 🌎 `Environment`
At step $t$, the **environment**:
- Receives action $A_t$
- Emits observation $O_{t+1}$ (and reward $R_{t+1}$)

Environment is about the **dynamics of the problem**

## ⚡️ `Rewards`
- Reward $R_t$ is scalar instant feedback signal
- Reward specifies the **goal**
- Cumulative reward = Return $G_t = R_{t+1}+R_{t+2}+R_{t+3}+... = \Sigma R_t$
- Agent's job is to **maximize the return $G_t$**

## 📊 `Values`
- Value $\nu(s)$ is expected cumulative reward, from state $s$
- $\nu(s)=\mathbb{E}[G_t\mid S_t=s]=\mathbb{E}[R_{t+1}+R_{t+2}+R_{t+3}+...\mid S_t=s]$
- The value depends on the actions the agent takes
- Goal is to **maximize value**, by picking suitable actions
- Recursive form
  - $G_t = R_{t+1}+G_{t+1}$
  - $\nu(s)=\mathbb{E}[R_{t+1}+\nu(S_{t+1})\mid S_t=s]$

## 𝑸 `Action values`
- Action value is value conditioned on **actions**
- Also known as **Q-value**
- $q(s,a)=\mathbb{E}[G_t\mid S_t=s,A_t=a]=\mathbb{E}[R_{t+1}+R_{t+2}+R_{t+3}+...\mid S_t=s, A_t=a]$
