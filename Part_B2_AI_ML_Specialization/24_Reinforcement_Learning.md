# 24. Reinforcement Learning

> **Part B2 — AI/ML Specialization** | SIU PET Complete Study Guide

---

## 24.1 Core Concepts

**Reinforcement Learning (RL):** An agent learns to make decisions by interacting with an environment, receiving rewards/penalties, and maximizing cumulative reward over time.

```
                    ┌──────────────┐
        action aₜ  │              │  reward rₜ
  Agent ──────────→│ Environment  │──────────→ Agent
    ↑              │              │              │
    │              └──────────────┘              │
    │                    │                       │
    │              state sₜ₊₁                   │
    └────────────────────┘                       │
                         ← learns from (sₜ, aₜ, rₜ, sₜ₊₁) ←
```

**Key terminology:**

| Term | Symbol | Description |
|------|--------|-------------|
| **Agent** | — | The learner/decision maker |
| **Environment** | — | The world the agent interacts with |
| **State** | $s \in S$ | Description of the current situation |
| **Action** | $a \in A$ | What the agent can do |
| **Reward** | $r \in \mathbb{R}$ | Immediate feedback (scalar signal) |
| **Policy** | $\pi(a|s)$ | Strategy: probability of action $a$ in state $s$ |
| **Value function** | $V^\pi(s)$ | Expected cumulative reward from state $s$ under policy $\pi$ |
| **Q-function** | $Q^\pi(s,a)$ | Expected cumulative reward from state $s$, taking action $a$, then following $\pi$ |
| **Discount factor** | $\gamma \in [0,1]$ | How much to value future rewards ($\gamma=0$: greedy, $\gamma=0.99$: far-sighted) |

**Return (cumulative discounted reward):**

$$G_t = r_t + \gamma r_{t+1} + \gamma^2 r_{t+2} + ... = \sum_{k=0}^{\infty} \gamma^k r_{t+k}$$

**RL vs. Supervised vs. Unsupervised:**

| Aspect | Supervised | Unsupervised | Reinforcement |
|--------|-----------|-------------|---------------|
| Feedback | Correct labels | None | Reward signal (delayed, sparse) |
| Data | i.i.d. samples | i.i.d. samples | Sequential, agent-generated |
| Goal | Predict labels | Find patterns | Maximize cumulative reward |

---

## 24.2 Markov Decision Process (MDP)

**Formal framework for RL.** Defined by tuple $(S, A, T, R, \gamma)$:

| Component | Description |
|-----------|-------------|
| $S$ | Set of states |
| $A$ | Set of actions |
| $T(s' \| s, a)$ | Transition probability: $P(s_{t+1}=s' \| s_t=s, a_t=a)$ |
| $R(s, a)$ | Reward function |
| $\gamma$ | Discount factor |

**Markov Property:** The future depends only on the current state, not the history:

$$P(s_{t+1} | s_t, a_t, s_{t-1}, a_{t-1}, ...) = P(s_{t+1} | s_t, a_t)$$

### Bellman Equations

**The foundation of most RL algorithms.**

**Bellman equation for value function:**

$$V^\pi(s) = \sum_a \pi(a|s) \left[ R(s,a) + \gamma \sum_{s'} T(s'|s,a) V^\pi(s') \right]$$

**Bellman optimality equation:**

$$V^*(s) = \max_a \left[ R(s,a) + \gamma \sum_{s'} T(s'|s,a) V^*(s') \right]$$

$$Q^*(s,a) = R(s,a) + \gamma \sum_{s'} T(s'|s,a) \max_{a'} Q^*(s',a')$$

**Intuition:** Optimal value = best immediate reward + discounted optimal future value.

### Model-Based vs Model-Free

| Type | Has Model of Environment? | Methods |
|------|--------------------------|---------|
| **Model-Based** | Yes (knows $T$ and $R$) | Dynamic Programming, Monte Carlo Tree Search |
| **Model-Free** | No (learns from experience) | Q-Learning, SARSA, Policy Gradient |

---

## 24.3 Dynamic Programming (Model-Based)

When the MDP is fully known:

**Value Iteration:** Iteratively update values using Bellman optimality equation until convergence:

$$V_{k+1}(s) = \max_a \left[ R(s,a) + \gamma \sum_{s'} T(s'|s,a) V_k(s') \right]$$

**Policy Iteration:** Alternate between:
1. **Policy Evaluation:** Compute $V^\pi$ for current policy
2. **Policy Improvement:** Make policy greedy with respect to $V^\pi$

---

## 24.4 Model-Free Methods

### 24.4.1 Temporal Difference (TD) Learning

**Combines ideas from Monte Carlo (learn from experience) and Dynamic Programming (bootstrap).**

$$V(s_t) \leftarrow V(s_t) + \alpha \underbrace{[r_t + \gamma V(s_{t+1}) - V(s_t)]}_{\text{TD error } \delta_t}$$

**TD error:** The difference between the new estimate ($r_t + \gamma V(s_{t+1})$) and the old estimate ($V(s_t)$).

| Method | Update After | Variance | Bias |
|--------|-------------|----------|------|
| **Monte Carlo** | End of episode | High (whole return) | Unbiased |
| **TD(0)** | Every step | Low (bootstrap) | Biased (uses estimate $V(s')$) |
| **TD(λ)** | Mix of both | Medium | Medium |

### 24.4.2 Q-Learning (Off-Policy)

**Learns the optimal Q-function directly, regardless of the current policy being followed:**

$$\boxed{Q(s_t, a_t) \leftarrow Q(s_t, a_t) + \alpha \left[ r_t + \gamma \max_{a'} Q(s_{t+1}, a') - Q(s_t, a_t) \right]}$$

**Off-policy:** The update uses $\max_{a'}$ (greedy), but the agent can follow a different policy (e.g., ε-greedy for exploration).

**Worked Example — Grid World:**

```
  ┌───┬───┬───┬───┐
  │ S │   │   │ G │    S = Start, G = Goal (+1 reward)
  ├───┼───┼───┼───┤    X = Pit (-1 reward)
  │   │ X │   │   │    Actions: ↑↓←→
  └───┴───┴───┴───┘
```

Initialize Q(s,a) = 0 for all states and actions. Episode: S→right→right→up→right→G.

After reaching G (reward=1), update Q backwards:
- Q(s=(0,2), a=right) ← 0 + 0.1[1 + 0.9·0 - 0] = 0.1
- Then in later episodes, these Q-values propagate backward through the grid.

### 24.4.3 SARSA (On-Policy)

**Follows the same policy it's learning:**

$$Q(s_t, a_t) \leftarrow Q(s_t, a_t) + \alpha \left[ r_t + \gamma Q(s_{t+1}, a_{t+1}) - Q(s_t, a_t) \right]$$

**Key difference:** Uses the actual next action $a_{t+1}$ (taken by the current policy) instead of $\max_{a'}$.

**Q-Learning vs SARSA:**

| Feature | Q-Learning | SARSA |
|---------|-----------|-------|
| Type | Off-policy | On-policy |
| Update | $\max_{a'} Q(s', a')$ | $Q(s', a')$ where $a'$ is actually taken |
| Convergence | To optimal $Q^*$ | To Q for the current policy |
| Exploration | More aggressive (ignores exploration in update) | More conservative (accounts for exploration) |
| Safety | May learn risky policies | Safer policies (considers ε-greedy behavior) |

---

## 24.5 Policy Gradient Methods

**Instead of learning value functions, directly learn the policy $\pi_\theta(a|s)$.**

### REINFORCE Algorithm

$$\nabla_\theta J(\theta) = E_\pi \left[ \sum_{t=0}^{T} \nabla_\theta \log \pi_\theta(a_t|s_t) \cdot G_t \right]$$

$$\theta \leftarrow \theta + \alpha \nabla_\theta J(\theta)$$

**Intuition:** Increase the probability of actions that led to high returns, decrease for low returns.

**Problem:** High variance (full episode returns are noisy). **Solution:** Subtract a baseline $b$ (typically $V(s)$):

$$\nabla_\theta J = E\left[\sum_t \nabla_\theta \log \pi_\theta(a_t|s_t) (G_t - b)\right]$$

### Actor-Critic

**Combines policy gradient (Actor) with value function (Critic):**

- **Actor** $\pi_\theta(a|s)$: Learns the policy (which action to take)
- **Critic** $V_\phi(s)$: Learns the value function (how good is this state)

**Advantage:** $A(s,a) = Q(s,a) - V(s) \approx r + \gamma V(s') - V(s)$ (TD error)

$$\theta \leftarrow \theta + \alpha \nabla_\theta \log \pi_\theta(a|s) \cdot A(s,a)$$

| Variant | Key Feature |
|---------|------------|
| **A2C** (Advantage Actor-Critic) | Synchronous, uses advantage function |
| **A3C** (Asynchronous A2C) | Multiple parallel agents for faster training |
| **PPO** (Proximal Policy Optimization) | Clips policy updates to prevent large changes — most popular |
| **SAC** (Soft Actor-Critic) | Maximizes reward + entropy (encourages exploration) |

**PPO** is today's default policy gradient algorithm. Key idea: don't let the policy change too much in one update. Uses a "clipped" objective:

$$L^{CLIP} = E\left[\min\left(r_t(\theta) A_t, \; \text{clip}(r_t(\theta), 1-\epsilon, 1+\epsilon) A_t\right)\right]$$

where $r_t(\theta) = \frac{\pi_\theta(a|s)}{\pi_{\theta_{old}}(a|s)}$ is the probability ratio.

---

## 24.6 Deep Reinforcement Learning

### 24.6.1 DQN (Deep Q-Network)

**Use a neural network to approximate $Q(s, a)$** instead of a table (handles continuous/large state spaces).

**Key innovations:**

| Technique | Problem Solved |
|-----------|---------------|
| **Experience Replay** | Stores $(s,a,r,s')$ transitions in a buffer, samples random mini-batches. Breaks correlation between consecutive samples. |
| **Target Network** | Separate, slowly-updated network for computing targets. Reduces instability from using the same network for both prediction and target. |

**DQN Algorithm:**
1. Take action using ε-greedy based on $Q_\theta(s,a)$
2. Store $(s, a, r, s')$ in replay buffer
3. Sample random batch from buffer
4. Compute target: $y = r + \gamma \max_{a'} Q_{\theta^-}(s', a')$ (using target network $\theta^-$)
5. Minimize loss: $(Q_\theta(s,a) - y)^2$
6. Periodically copy $\theta → \theta^-$

### 24.6.2 Notable Deep RL Achievements

| System | Year | Achievement | Methods |
|--------|------|-------------|---------|
| **DQN** (DeepMind) | 2013 | Atari games at superhuman level | Deep Q-Network |
| **AlphaGo** | 2016 | Beat world champion at Go | MCTS + supervised + RL |
| **AlphaZero** | 2017 | Master Chess, Go, Shogi from scratch | Self-play + MCTS |
| **OpenAI Five** | 2019 | Beat world champions at Dota 2 | PPO, massive scale |
| **ChatGPT/RLHF** | 2022 | Align LLMs with human preferences | PPO + reward model |

---

## 24.7 Exploration vs. Exploitation

**The fundamental dilemma:** Exploit (choose best known action) vs. Explore (try unknown actions to find better ones).

| Strategy | Description | Pros/Cons |
|----------|-------------|-----------|
| **ε-greedy** | With prob ε, take random action; else take best | Simple, but explores uniformly (wastes time on bad actions) |
| **ε-decay** | Decrease ε over time (explore less as learning progresses) | Better: explore early, exploit later |
| **UCB** | Choose $a = \arg\max \left[Q(a) + c\sqrt{\frac{\ln t}{N(a)}}\right]$ | Explores under-tried actions proportionally |
| **Boltzmann (softmax)** | $P(a) = \frac{e^{Q(a)/\tau}}{\sum e^{Q(a')/\tau}}$ with temperature $\tau$ | Smooth exploration, temperature controlled |
| **Thompson Sampling** | Sample from posterior of reward distribution | Bayesian, optimal for bandits |

---

## 24.8 Practice Questions

**Q1.** Explain the difference between Q-Learning and SARSA. When would SARSA be preferred?
> **Answer:** Both learn Q-values, but differ in the update target. **Q-Learning (off-policy):** $Q(s,a) \leftarrow Q(s,a) + \alpha[r + \gamma \max_{a'} Q(s',a') - Q(s,a)]$ — uses the maximum Q-value (optimal action) regardless of what action was actually taken. **SARSA (on-policy):** $Q(s,a) \leftarrow Q(s,a) + \alpha[r + \gamma Q(s',a') - Q(s,a)]$ — uses the Q-value of the action actually taken (including exploration). **SARSA preferred when:** Safety matters. In a cliff-walking problem, Q-Learning learns the optimal path (close to cliff edge) because it assumes greedy behavior. SARSA learns a safer path (further from cliff) because it accounts for the ε-greedy exploration that might cause falls. In robotics or real-world applications where exploration mistakes are costly, SARSA is safer.

**Q2.** What is the Bellman equation and why is it central to RL?
> **Answer:** The Bellman equation expresses the value of a state as the immediate reward plus the discounted value of the next state: $V^*(s) = \max_a[R(s,a) + \gamma \sum_{s'} T(s'|s,a) V^*(s')]$. It provides a recursive decomposition that turns the RL problem into smaller subproblems. **Central because:** (1) Dynamic Programming algorithms (Value Iteration, Policy Iteration) directly solve it; (2) TD learning uses it to bootstrap updates; (3) Q-Learning is derived from the Bellman optimality equation for Q-values; (4) It guarantees convergence — iteratively applying the Bellman operator is a contraction mapping that converges to the unique fixed point $V^*$.

**Q3.** Explain DQN. What are experience replay and target networks, and why are they needed?
> **Answer:** DQN uses a neural network to approximate $Q(s,a)$ for large state spaces (e.g., Atari game pixels). Two problems arise with naive neural network Q-learning: (1) **Correlated samples:** consecutive game frames are highly correlated → unstable training. **Experience replay** solves this by storing transitions in a buffer and sampling random mini-batches, breaking temporal correlations. (2) **Moving target:** the same network is used for both the Q-value prediction and the target ($r + \gamma \max Q(s',a')$) — updating the network changes both, causing oscillation. **Target network** solves this by maintaining a separate, slowly-updated copy ($\theta^-$) for computing targets, updated every $C$ steps.

**Q4.** What is the advantage function in Actor-Critic methods? Why is it better than using raw returns?
> **Answer:** The advantage function $A(s,a) = Q(s,a) - V(s)$ measures how much better action $a$ is compared to the average action in state $s$. **Why better than raw returns $G_t$:** Raw returns have high variance because they depend on all future randomness (many future states and rewards). The advantage function subtracts the baseline $V(s)$, which removes the variance due to the state's inherent value. If a state is inherently valuable, all actions get high $G_t$ — the advantage correctly identifies which actions are above or below average. This dramatically reduces variance while keeping the gradient estimate unbiased (or nearly so), leading to faster, more stable training.

**Q5.** How is RL used in RLHF (Reinforcement Learning from Human Feedback) for training LLMs like ChatGPT?
> **Answer:** RLHF has three stages: (1) **Supervised fine-tuning:** Fine-tune a pre-trained LLM on human-written demonstrations. (2) **Reward model training:** Collect human preferences (rank multiple model outputs for the same prompt), train a reward model to predict human preferences. (3) **RL fine-tuning:** Use PPO to optimize the LLM policy to maximize the reward model's score, with a KL divergence penalty to prevent the model from deviating too far from the supervised fine-tuned model. The KL penalty is crucial — without it, the model would "hack" the reward model by producing adversarial outputs that score high but are nonsensical.

---

*Previous: [Chapter 23 — Computer Vision](23_Computer_Vision.md) | Next: [Chapter 25 — Data Mining & Big Data](25_Data_Mining_and_Big_Data.md)*
