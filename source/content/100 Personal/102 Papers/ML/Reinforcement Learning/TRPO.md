#RL #ML #AI
## Overall Objective

TRPO was introduced to be able to implement an RL algorithm that remained stable under policy gradient updates ^280755

### Objective Function

First, let's take a look at the objective function and break down what TRPO is trying to do

$$
\max_{\theta} \mathbb{E}_{t} \left[ \frac{\pi_{\theta}(a_t | s_t)}{\pi_{\theta_{\text{old}}}(a_t | s_t)} \hat{A}_t \right]
$$

Now lets break it down piece-by-piece and try to intuitively understand the different pieces


### Reward Comparison

First lets take a look at the reward policy comparison

$$
\frac{\pi_{\theta}(a_t | s_t)}{\pi_{\theta_{\text{old}}}(a_t | s_t)}
$$

The policy functions are represented as $\pi_{\theta}$ and the old policy as $\pi_{\theta_{\text{old}}}$. so when we divide the two, we are essentially calculating the ratio between them. This tells us by how much the parameters or the policy has changed from the old policy to the current one. The further we are away from 1, the more change is exhibited

### Advantage Function

The advantage function ($\hat{A}$) is the difference between **current action taken** and the **action predicted by the policy**. The more positive the $\hat{A}$ is , the more that the current action outperforms the policy's predicted action (and vice versa). 

### To put it all together

If come back to the objective function

$$
\max_{\theta} \mathbb{E}_{t} \left[ \frac{\pi_{\theta}(a_t | s_t)}{\pi_{\theta_{\text{old}}}(a_t | s_t)} \hat{A}_t \right]
$$

We are trying to maximize the multiplication of the rate of change between the policies and the advantage. Intuitively, this means we are trying to incentivize the policy changes that lead to better advantages

## The key to TRPO

The key to TRPO is the constraint we have to adhere to

$$
\mathbb{E}_{t} \left[ {\text{KL}} \left( \pi_{\theta_{\text{old}}}(a_t | s_t) \| \pi_{\theta}(a_t | s_t) \right) \right] \leq \delta
$$
the $\left[ {\text{KL}} \left( \pi_{\theta_{\text{old}}}(a_t | s_t) \| \pi_{\theta}(a_t | s_t) \right) \right]$ represents the difference in the distributions of the old and current policy. We are then making sure that this difference is greater than some $\delta$, ensuring we are not make steps that are **too large**. This works to keep the algorithm stable