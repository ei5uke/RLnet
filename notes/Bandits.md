# k-armed Bandits
> Consider the following learning problem. You are faced repeatedly with a choice among k different options, or actions. After each choice you receive a numerical reward chosen from a stationary probability distribution that depends on the action you selected. Your objective is to maximize the expected total reward over some time period, for example, over 1000 action selections, or ==[[Vocab#timestep t|timestep]]==. This is the original form of the k-armed bandit problem, so named by analogy to a slot machine, or "one-armed bandit," except that it has k levers instead of one.

\- Sutton & Barto RL Book, 25-26

### Gist
In other words, from a selection of *k* actions, one must learn which actions would return the best ==[[Vocab#reward R_t|reward]]==.  Let's say over 3 timesteps, we choose action *n* all 3 times. An example sequence may be with timestep 1, we received a reward of 1, with timestep 2, a reward of 0, and with timestep 3 a reward of 0.5. However, let's say we chose action *m* all 3 times, we may get rewards of -1, -2, and -3 instead. We can see that choosing different actions result in different rewards.

What happens if we pick both action *n* and *m* during different timesteps? That is, let's say we pick action *n* on timestep 1, but action *m* on timestep 2 and 3. On timestep 1, we'll receive a reward of 1 like before, but on timestep 2 and 3 we may receive different rewards. In an essence, the idea of k-armed bandits is to figure out when to pick which specific action to receive the most amount of rewards. 

Our solution to this is to associate each bandit having a ==[[Vocab#value|value]]==, or an expected reward. Our value, or expected reward, is denoted $q_*(a) = 𝔼[R_t | A_t = a]$ where $a$ is an arbitrary action taken for action $A_t$ at timestep $t$ and we received a reward of $R_t$. $q_*(a)$ is our true value, however, in many scenarios, we do not know what it is. And so, we use an estimated value, $Q_t(a)$ to keep track of our values and update it to get as close to our true value, $q_*(a)$. We denote $Q_t(a)$ as:

$$Q_t(a) = \frac{\text{sum of rewards when a taken prior to t}}{\text{number of times a taken prior to t}}$$

which is our current mean of rewards of action $a$.

So far, we have a means to know how well certain actions perform compared to others, and so we now need a method to distinguish which action to choose from our choice of k-bandits. One way is to have an ε-greedy method, which ==[[Vocab#exploit|exploits]]== with ε probability, and otherwise ==[[Vocab#explore|explores]]==. This exploiting behavior is called ==[[Vocab#greedy|greedy]]==. We denote the exploiting action as $A_t = argmax_a Q_t(a)$ where we choose the action $a$ that gives us the maximum value, $Q_t$. We have to strike a balance between when to exploit and explore. If we exploit all the time, we are not giving chances to other actions which may perform better later on. However, if we explore all the time, we are wasting timesteps on unoptimal actions.

###### Example
Let's say we have 2 bandits and at timestep 0, they start with 0 rewards. Let's say we have this sequence: $A_1 = 1, R_1 = 1, A_2 = 2, R_2 = 1, A_3 = 1, R_3 = 1, A_4 = 1, R_4 = 2$. The following table represents the value of a bandit at each timestep.

timestep | bandit 1 | bandit 2
-- | -- | --
0 | 0 | 0
1 | 1 | 0
2 | 1 | 1
3 | 1 | 1
4 | 1.67 | 1

To explain the values of bandit 1, at timestep 1 it received a return of 1, and so it gets initialized as such. For timesteps 2 and 3, it maintains its value because it has not been selected. For timestep 4, it receives a reward of 2, and so since the value is $\frac{\text{sum of rewards taken prior to t}}{\text{number of times taken prior to t}}$, it is $\frac{1 + 2}{2}$ or $1.67$. For bandit 2, although it receives two rewards, since the sum is 2 and it was picked twice, the value is still 1.

%%
Probably add pages 30-41 later
%%