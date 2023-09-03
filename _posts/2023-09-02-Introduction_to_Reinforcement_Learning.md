---
layout: post
title:  "Introduction to Reinforcement Learning"
categories:
  - deepmind_lecture
tags:
  - [Deepmind RL Lecture]
date: 2023-09-03
last_modified_at: 2023-09-03
---

<img src="/assets/DeepMind_UCL_RL_slides/Lecture 1 - introduction/Lecture 1 - introduction-01.png" width=1000/>

<img src="/assets/DeepMind_UCL_RL_slides/Lecture 1 - introduction/Lecture 1 - introduction-20.png" width=1000/>

## Agent and Environment

<img src="/assets/DeepMind_UCL_RL_slides/Lecture 1 - introduction/Lecture 1 - introduction-21.png" width=1000/>

### Agent
- Input: Observation, Reward
- Output: Action
    
### Environment
- Input: Action
- Output: Observation, Reward

## Rewards

<img src="/assets/DeepMind_UCL_RL_slides/Lecture 1 - introduction/Lecture 1 - introduction-22.png" width=1000/>

### Reward
- instant feedback signal for a step

### Return
- cumulative reward = total sum of reward in a episode

**Agents need to learn how to maximize the return**

## Values

<img src="/assets/DeepMind_UCL_RL_slides/Lecture 1 - introduction/Lecture 1 - introduction-23.png" width=1000/>

### Values
- expected return from state s

## Action values

<img src="/assets/DeepMind_UCL_RL_slides/Lecture 1 - introduction/Lecture 1 - introduction-25.png" width=1000/>

### Action values
- = Q-value
- cumulative reward conditioned on both actions and states

# Agent

<img src="/assets/DeepMind_UCL_RL_slides/Lecture 1 - introduction/Lecture 1 - introduction-27.png" width=1000/>

<img src="/assets/DeepMind_UCL_RL_slides/Lecture 1 - introduction/Lecture 1 - introduction-28.png" width=1000/>

