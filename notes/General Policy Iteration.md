# General Policy Iteration
### Intro
GPI is a method used to update a given policy in order to find a better policy. It achieves this by combining two ideas: [[General Policy Iteration#Policy Evaluation|Policy Evaluation]] and [[General Policy Iteration#Policy Improvement|Policy Improvement]]. By combining these ideas and applying them repeatedly in [[General Policy Iteration#GPI|GPI]], we can slowly but surely approach the optimal policy, and converge to the optimal policy.

The concept of GPI is key in understanding tabular methods, specifically [[Dynamic Programming]], [[Monte Carlo]], and [[Temporal Difference]]

### Policy Evaluation
Before we want to find a better policy, we first have to ask a question to ourselves: Is our current policy already the optimal policy? Policy Evaluation gives us our answer by calculating the state value of a state when using our current policy, and by doing so, we can see how effective our current policy is. Let's say we have state $s$ and before we start evaluating it, we initialize it a value of 0:
$$v_{0}(s) = 0$$ 
Note that we have a subscript of 0 to detail that this is our initial state value of state $s$. To evaluate it, we follow our current policy behavior for the state, then initialize our next evaluation with this value: 
$$v_{1}(s) = 𝔼_{π}[R_{t+1} + γv_{0}(S_{t+1}) | S_{t} = s]$$
Now that we have the 1st evaluation, we continue this, applying the policy again and initalizing our next evaluation with this value. We repeat this again and again and have this generalized equation:
$$v_{k+1}(s) = 𝔼_{π}[R_{t+1} + γv_{k}(S_{t+1}) | S_{t} = s]$$
As $k \to \infty$, $v_{k} \to v_{π}$, and it eventually converges to $v_{π}$, giving us the true value of the state.
### Policy Improvement
Now that we know how to evaluate a certain policy, we want to see whether we can improve it and find a better one. Perhaps our current policy is generally good, but given a certain state, its performance worsens. Thus, we may want to take a specific action during this one state, one not generally picked by our stochastic policy (somewhat going against our policy), and then continue using our policy again later on. This is the general idea of Policy Improvement; we want to build upon our current policy and steadily improve it. 
To see this idea mathematically, we are essentially taking an action $a$ and then following up with policy $π$ thereafter, in other words, an action value:
$$q_{π}(s,a)= 𝔼[R_{t+1} + γv_{π}(S_{t+1})| S_{t} = s, A_{t} = a]$$
Now, we want to find a new policy $π'$ that is better or equal to our current policy, so we get the policy that is greedy according to our action value:
$$π'(s) = \underset{a}{argmax}q_{π}(s, a)$$
Now that we have a new policy, we compare it to our old one. If $q_{π'} > v_{π}$, then we effectively know that $π'$ is better than $π$. With this, we found the policy better than or equal to our current one, and can improve our policy. Remember that we are only acting greedy in this one state and action, and so we have only changed the policy in this one instance and not the entire policy itself. Thus, we can see how we take small increments in improving the policy by updating at specific state-action pairs.

### GPI
Iteratively applying the two features from before (evaluating, improving, evaluating, improving, ...) we can update our policy closer to the optimal policy:
$$π_{0}\overset{E}{\to}v_{π_{0}}\overset{I}{\to}π_{1}\overset{E}{\to}v_{π_{1}}\overset{I}{\to}{\cdots}\overset{I}{\to}{π_{*}}\overset{E}{\to}{v_{π_{*}}}$$
This is what General Policy Iteration is. However, it is clear that a repetition of a complete evaluation and improvement will be computationally costly. Not only must we continue iterating $k$ for a long time until we coincidentally reach $π$, but given an environment with $n$ states, we repeat this action for all states. To speed up the computation, we can just *not* complete evaluation. Every time we perform policy evaluation, we can iterate once to improve it once, rather than iterating until we converge to $π$. As long as we *approach* $π$ every iteration during GPI, we effectively converge to the optimal policy $π_{*}$. 
