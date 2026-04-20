# 24. Reinforcement Learning

> **Part B2 — AI/ML Specialization** | SIU PET Study Guide

---

- [ ] **Core Concepts**
  - Agent, environment, state, action, reward
  - Policy (π): Mapping from states to actions
  - Value function: Expected future reward V(s) or Q(s,a)
  - Discount factor (γ): How much future rewards matter

- [ ] **Markov Decision Process (MDP)**
  - States S, Actions A, Transition function T(s'|s,a), Reward R(s,a), Discount γ
  - Markov property: Future depends only on current state
  - Bellman equation: $V(s) = \max_a [R(s,a) + \gamma \sum T(s'|s,a) V(s')]$

- [ ] **Model-Free Methods**
  - **Q-Learning** (off-policy):
    - $Q(s,a) \leftarrow Q(s,a) + \alpha [r + \gamma \max_{a'} Q(s',a') - Q(s,a)]$
  - **SARSA** (on-policy):
    - $Q(s,a) \leftarrow Q(s,a) + \alpha [r + \gamma Q(s',a') - Q(s,a)]$
  - **Temporal Difference (TD) Learning**: Update at each step, not end of episode

- [ ] **Policy Gradient Methods**
  - Learn the policy directly
  - REINFORCE algorithm
  - Actor-Critic: Actor (policy) + Critic (value function)
  - A2C, A3C, PPO (Proximal Policy Optimization)

- [ ] **Deep Reinforcement Learning**
  - **DQN** (Deep Q-Network): Neural network for Q-value function
    - Experience replay: Store transitions, sample randomly
    - Target network: Stabilize training
  - **AlphaGo/AlphaZero**: Monte Carlo Tree Search + Deep RL

- [ ] **Exploration vs. Exploitation**
  - ε-greedy: Explore with probability ε, exploit otherwise
  - UCB (Upper Confidence Bound)
  - Thompson sampling
  - Multi-armed bandit problem

---

### Recommended Resources
- **Book**: *Reinforcement Learning: An Introduction* — Sutton & Barto (free online)
- **Course**: David Silver's RL course (DeepMind, YouTube)
