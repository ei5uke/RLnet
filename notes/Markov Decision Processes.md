# Markov Decision Processes
### Gist
In MDP's, rather than consisting only of bandits, we have an ==[[Vocab#agent|agent]]== that interacts with an ==[[Vocab#environment|environment]]==. The two of them have a feedback loop, where there is a certain state $S_t$ of the environment (e.g., a certain frame in a game), the agent receives it and performs a certain action $A_t$ (e.g., our agent performs a jump action), and the environment responds back with the next state $S_{t+1}$ and the next reward $R_{t+1}$. Alongside those, we also have $p$, or the ==[[Vocab#dynamics p|dynamics]]== of the MDP, which determine the probability a certain state and reward are returned given a certain state and action, denoted:
$$p(s', r | s, a) = Pr\{S_t = s', R_t = r | S_{t-1} = s, A_{t-1} = a\}$$

The key feature of a MDP is the ==*[[Vocab#markov property|Markov Property]]*==, which is when "the state must include information about all aspects of the past agent-environment interaction that make a difference for the future" (Sutton & Barto, 49). 

Similar to bandits, in MDP's the goal is to find actions that give us the most rewards. We can depict the sum of all rewards as $R_{t} + R_{t+1} + ... + R_{T} = G_{t}$, which we call the ==[[Vocab#expected return G_ t|expected return]]== at timestep $t$. 

Given a ==[[Vocab#discount rate γ|discount rate]]==, we can rewrite the expected return formula to the following:
$$G_{t} = R_{t+1} + γR_{t+1} + ... + γR_{T} = R_{t+1} + γG_{t+1}$$
which works even when it's an episodic task by setting $γ$ to 1 on all non-terminal states and 0 on the terminal state.

From all this info, we can now create the MDP version of values: state values and action values.

The ==[[Vocab#state value|state value]]== is the value of a state $s$ under a policy $π$, or the expected return when starting in state $s$ and following policy $π$, denoted:
$$v_{π}(s) = 𝔼_{π}[G_{t}|S_{t}=s]$$

The ==[[Vocab#action value|action value]]== is the value, or expected return, of taking action $a$ given state $s$ under policy $π$, denoted:
$$q_{π}(s,a) = 𝔼_{π}[G_{t}|S_{t}=s, A_{t}=a]$$

We want to continue finding policies that are better than our current policy, and the goal of MDP's is to find the ==[[Vocab#optimal policy|optimal policy]]==, denoted $π_{*}$.

**Example**
blob add later