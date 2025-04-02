#RL #ML #AI
> A policy is a state-action mapping. A 'state' is a formalism used in AI that represents the state of the world, i.e. what the agent's idea of the world is. The action is, naturally, what action it should take in that state. A policy just maps states to actions.


The Policy network is the network that is trying to maximize the amount of rewards it gets from the environment

Some of the earliest RL algorithms that made a big breakthrough was DQN, developed by **DeepMind**. The problem was that DQN was very **unstable**

This motivated the development of **TRPO**

Below is a deeper dive into TRPO

![[TRPO#^280755]]

One of the major drawbacks of TRPO, however, was that it was very compute heavy. that is what PPO aimed to accomplish, by simplifying the function. 

### Objective Function

The objective function is as follows, where $r_t(\theta)$ = $\frac{\pi_{\theta}(a_t | s_t)}{\pi_{\theta_{\text{old}}}(a_t | s_t)}$, and $\epsilon$ = 0.2

$$
L^{CLIP}(\theta) = \mathbb{E}_t \left[ \min \left( r_t(\theta) \hat{A}_t, clip \left( r_t(\theta), 1 - \epsilon, 1 + \epsilon \right) \hat{A}_t \right) \right]

$$

Let's break this down piece-by-piece
$$
clip \left( r_t(\theta), 1 - \epsilon, 1 + \epsilon \right) \hat{A}_t)
$$

Here, we are clipping the reward incentive $r_t(\theta)$ between 0.8 and 1.2, so we ensure that our steps are not too large

$$
\min \left( r_t(\theta) \hat{A}_t, clip \left( r_t(\theta), 1 - \epsilon, 1 + \epsilon \right) \hat{A}_t \right)
$$

We now take the minimum of $r_t(\theta) \hat{A}_t$ and the clipped version of $r_t(\theta) \hat{A}_t$. We do this so that we can take the minimum possible step, and therefore the safest step in the right direction of the policy gradient space. 