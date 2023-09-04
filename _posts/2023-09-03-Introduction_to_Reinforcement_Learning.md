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

# Formalising the RL Problem

<p align="center"><img src="/assets/DeepMind x UCL RL Lecture/agent_env.png" width=550></p>

## 🧠 `Agent`
At step $t$, the **agent**:
- Receives observation $O_t$ (and reward $R_t$)
- Executes action $A_t$

Agent contains:
- Agent state
- Policy
- Value function estimate
- Model

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
- Recursive form
  - $G_t = R_{t+1}+G_{t+1}$

## 📊 `Values`
- Value $\nu(s)$ is expected cumulative reward, from state $s$
- $\nu(s)=\mathbb{E}[G_t\mid S_t=s]=\mathbb{E}[R_{t+1}+R_{t+2}+R_{t+3}+...\mid S_t=s]$
- The value depends on the actions the agent takes
- Goal is to **maximize value**, by picking suitable actions
- Recursive form
  - $\nu(s)=\mathbb{E}[R_{t+1}+\nu(S_{t+1})\mid S_t=s]$

## 𝑸 `Action values`
- Action value is value conditioned on **actions**
- Also known as **Q-value**
- $q(s,a)=\mathbb{E}[G_t\mid S_t=s,A_t=a]=\mathbb{E}[R_{t+1}+R_{t+2}+R_{t+3}+...\mid S_t=s, A_t=a]$

# Inside the Agent: the Agent State
## 🎮 `Agent states`
- $\neq$ Environment state
- Environment state is usually invisible to the agent
- Even if it is visible, it may contain lots of irrelevant information
- History $\mathcal{H}_t$ is full sequence of observations, actions, and rewards
- $\mathcal{H}_t=O_0, A_0, R_1, O_1, A_1,R_2 ..., O_t$
- History is used to construct the agent state $S_t$
- When the environment is **fully observable**,
  - Observation = Environment state
  - $S_t=O_t=$ environment state
 
## 🤖 `Markov decision processes`
- MDP is used to formulate reinforcement learning problems
- A decision process is Markovian if:
  - $p(r, s, \mid S_t, A_t)=p(r, s \mid \mathcal{H}_t, A_t)$
  - Probability of a reward and a subsequent state doesn't change either if we add more history or not
- The state $S_t$ contains all we need to know from the history $\mathcal{H}_t$
- Doesn't mean $S_t$ contains everything, just adding more $\mathcal{H}_t$ doesn't help
- Agent state $S_t$ is some compression of $\mathcal{H}_t$
- Note: $S_t=$ agent state $\neq$ environment state
- **Partial observability**
  - When the agent is partially observable,  **the observations are not Markovian**
  - ex1) A robot with camera vision isn't told its absolute location
  - ex2) A poker playing agent only observes public cards
  - In this situation, using the observation as state would not be Markovian
  - This process is called **partially observable Markov decision process (POMDP)**
  - Note that the **environment state** can still be Markov, but the agent doesn't know it
  - Also, note that we can still be able to construct a Markov agent state
    - For example, by giving the full history $\mathcal{H}_t$ instead of single state can make agent Markovian
- **Agent state**
  - The agent's actions depend on its state
  - The agent state is function of the history
  - For instance, $S_t=O_t$
  - Generally: $S_{t+1}=u(S_t, A_t, R_{t+1}, O_{t+1})$
    - Where $u$ is a "state update function"
  - The agent state is often **much smaller** than the environment state
- To deal with partial observability, agent can construct suitable state representations
- Examples of agent states:
  - Last observation: $S_t=O_t$ (might not be enough)
  - Complete history: $S_t=\mathcal{H}_t,$ (might be too large)
  - A generic update: $S_t=u(S_t, A_t, R_{t+1}, O_{t+1})$ (but how to pick/learn $u$?)
- Constructing a fully Markovian agent state is often not feasible
  - ex) The observation might be really complicated, might be hard to construct full Markovian

# Inside the Agent: the Policy
## 𝝅 `Policy`
- Policy defines the agent's behavior
- Map from agent state to action
- Deterministic policy: $A = \pi(S)$
- Stochastic policy: $\pi(A \mid S) = p(A \mid S)$

# Inside the Agent: Value Estimates
## 𝜈 `Value Functions`
- The actual value function is **expected return**
  - $\nu_{\pi}(s) = \mathbb{E}[G_t \mid S_t = s, \pi]= \mathbb{E}[R_{t+1}+\gamma R_{t+2} +\gamma^2 R_{t+3}+... \mid S_t = s, \pi]$
  - **Discount factor** ($\gamma \in [0, 1]$) trades off importance of immediate vs long-term rewards
    - If $\gamma$ is close to 0, it gives more weight in immediate reward and *vice versa*
- The value depends on a policy $\pi$
- Can be used to evaluate desirability of states
- Can be used to select between actions
- As is in reward function, value function can be formulate in recursive form as well
  - $\nu_{\pi}(s)=\mathbb{E}[R_{t+1}+\gamma G_{t+1} \mid S_t = s, A_t \sim \pi(s)]=\mathbb{E}[R_{t+1}+\gamma \nu_{\pi}(S_{t+1}) \mid S_t = s, A_t \sim \pi(s)]$
  - $a \sim \pi(s)$ means $a$ is chosen by policy $\pi$ in state $s$ (even if $\pi$ is deterministic)
  - The above equation is known as a **Bellman equation**
  - Similar equation holds for the optimal (=highest possible) value:
    - $\nu_{\ast}(s)=\max_a \mathbb{E}[R_{t+1}+\gamma \nu_{\ast}(S_{t+1}) \mid S_t = s, A_t=a]$
    - This equation **does not** depend on a policy
    - We heavily exploit such equalities, and use them to create algorithms

# Inside the Agent: Models
## 💃 `Model`
- A model predicts what the environment will do next
  - ex1) $\mathcal{P}$ predicts the **next state**
    - $\mathcal{P}(s, a, s')\approx p(S_{t+1}=s' \mid S_t=s, A_t=a)$
  - ex2) $\mathcal{R}$ predicts the **next (immediate) reward**
    - $\mathcal{R}(s, a)\approx \mathbb{E}[R_{t+1} \mid S_t = s, A_t=a]$
- A model does not immediately give us good policy: we still need to **plan**
- **stochastic (generative) model** is also considerable

# Agent Categories
- Value based
  - No policy (Implicit)
  - Value function
- Policy based
  - Policy
  - No value function
- Actor Critic
  - Policy
  - Value function

- Model free
  - Policy and/or Value funciton
  - No model
- Model based
  - (Optionally) Policy and/or Value funciton
  - Model
