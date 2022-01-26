The purpose of this doc is to provide definitions to a list of common words. Use `ctrl+f` or `cmd+f` to search through this doc and find any specific word.

##### action value
the expected return, of taking action $a$ given state $s$ under policy $π$, $q_{π}(s,a) = 𝔼_{π}[G_{t}|S_{t}=s, A_{t}=a]$
##### agent
the object that learns and chooses actions
##### bellman equation
state-value: $v_{π}(s)=\displaystyle \sum_{a} π(a|s) \displaystyle \sum_{s',r} p(s',r|s,a)[r+γv_{π}(s')]$
action-value: $v_{π}(s)=\displaystyle \sum_{a} π(a|s) \displaystyle \sum_{s',r} p(s',r|s,a)[r+γq_{π}(s',a')]$
##### bellman optimality equation
state-value: $v_{**}(s)=\text{max}_{a}\displaystyle \sum_{s',r} p(s',r|s,a)[r+γv_{*}(s')]$
action-value: $v_{**}(s)=\displaystyle \sum_{s',r} p(s',r|s,a)[r+γ\text{max}_{a'}q_{*}(s')]$
##### continuing tasks
MDP's where episodes do not naturally distinguish from each other
##### discount rate $γ$
The rate that gets applied to future rewards, generally within [0, 1]
##### dynamics $p$
probability a certain state and reward are returned given a certain state and action
##### environment
everything that exists aside from the agent
##### episode
a sequence of agent-environment interactions
##### episodic task
MDP's where episodes end in a terminal state
##### expected return $G_{t}$
the sum of all rewards from timestep $t$ to terminal state
##### exploit
choose best action according to current knowledge
##### explore
try out unknown actions, e.g., sample a random action
##### greedy
behavior where we exploit
##### markov property
when a state includes details about past interactions which influence the future
##### optimal policy $π_{*}$
the policy (or policies) that are better than or equal to all other policies
##### policy $π$
a mapping from states to probabilities of selecting each possible action; i.e., how an agent behaves
##### state value
the expected return when starting in state $s$ and following policy $π$, $v_{π}(s) = 𝔼_{π}[G_{t} | S_{t} = s]$
##### timestep $t$
an action selection, or one sequence of a state and an action.
##### reward $R_t$
an amount received after performing a certain action given a certain state
##### value
average rewards of a specific action in a specific state, $q(a) = 𝔼[R_t | A_t = a]$