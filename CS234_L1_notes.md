## Reinforcement Learning Seminar
> Materials:
>
>  [Mr. Sutton's Book 2018](http://incompleteideas.net/book/the-book.html)
>
> [CS234 Winter 2018 lecture notes](http://web.stanford.edu/class/cs234/schedule.html)



### Lecture 1 (2018.06.11~2018.06.24)

#### Intro


Repeated Interactions with World

Learn to make good <span style="color:yellow">sequences</span> of decisions under <span style="color:yellow">uncertainty</span>.

Involves:

* Optimization -> find an optimal way to make decisions yielding best outcomes or at least very good strategy
* Delayed consequences -> Decision now can impactthings much later
* Exploration -> Learning about the world by making decisions
* Generalization

<span style="color:yellow">Policy</span> is mapping from past experience to Interactions

<span style="color:red">Why not just pre-program a policy?</span>

Comparison:

RL vs (key: explore the world, use experience to guide future decisions)
* AI planning
* Supervised Learning
* Unsupervised Learning
* Imitation Learning

Other issues:

* Where do rewards come from? And what happens if we get it wrong?
* Robustness / risk sensitivity
* Multi-agent RL

#### SDM (Sequential Decision Making)

* Each time $t$, agent takes an action $a_t$;
world updates given action $a_t$, emits observations $o_t$, reward $r_t$;
agent receives observation $o_t$ and reward $r_t$
* History $h_t=(a_1,o_1,r_1,...,a_t,o_t,r_t)$;
state is information assumed to decide what happens next: $s_t=(h_t)$

Goal: select actions to maximize total expected future reward.

May require balancing immediate & long term rewards.
<span style="color:lightgreen">May require strategic behavior to achieve high rewards.</span>

#### Markov Definitions
State $s$ is **Markov** is and only if future is independent of past given present:
$$
P(S_{t+1}|s_t,a_t) = P(s_{t+1}|h_t,a_t)
$$

Why is Markov Assumption Popular?
* Can always be satisfied
  * <span style="color:red"> Setting status as history always Markov</span>

* In practice often assume most recent observation is <span style="color:yellow"> sufficient statistic</span> of history $s_t = o_t$

* State representation has big implication for
    * Computation complexity
    * Data required
    * Resulting performance


**Full Observability / MDP**
* $s_t = o_t$

**Partial Observability / POMDP**
* Agent state is not the same as world State
* Agent constructs its own state eg use history $s_t=h_t$, or beliefs of world state, or RNNs
* Eg Poker player, healthcare

#### Types of Sequential Decision Processes:
* Bandit(no delayed influence)
* MDP / POMDP
* How the world changes (deterministic or stochastic)

RL Agent Component often include on or more of
* Model
* Policy
* Value function

#### Model
* agent's representation of how the world changes in response to agent's action
* Transition /dynamics model predicts next agent state: $P(s_{t+1}=s'|s_t=s,a_t=a)$
* Reward model predicts immediate reward: $R(s_t=s,a_t=a)=E(r_t|s_t=t,a_t=1)$
* Policy determines how the agent chooses actions: $\Pi:S\rightarrow A$,
deterministic policy $\Pi(s)=a$, stochastic policy $\Pi(a|s) = P(a_t=a|s_t=s)$
* Value function $V^{\Pi}$: expected discounted sum of future rewards under a perticular Policy

#### Types of Agents (David Silver)
* value based
  * Explicit: value function
  * implicit: Policy( can derive a policy from value function)

* policy based
  * Explicit: policy
  * No value function

* Actor critic
  * Explicit: Policy
  * Explicit: value function

* Model based
  * Explicit: Model
  * may or may not have policy and /or value function

* Model free
  * Explicit: value function
  * No model
