# POLICY ITERATION ALGORITHM

## AIM :
To implement a policy iteration algorithm for the given MDP.

## PROBLEM STATEMENT :
The problem statement is a Five stage slippery walk where there are five stages excluding goal and hole.The problem is stochastic thus doesnt allow transition probability of 1 for each action it takes.It changes according to the state and policy.

### STATE SPACE :
The states include two terminal states: 0-Hole[H] and 6-Goal[G]. It has five non terminal states including starting state.

### ACTION SPACE :
Left:0

Right:1

### TRANSITION PROBABILITY :
The transition probabilities for the problem statement is:

50% - The agent moves in intended direction.

33.33% - The agent stays in the same state.

6.66% - The agent moves in orthogonal direction.

### REWARD :
To reach state 7 (Goal) : +1 otherwise : 0

### GRAPHICAL REPRESENTATION :
![image](https://github.com/obedotto/policy-iteration-algorithm/assets/113497395/e10d6a93-d6e5-4dca-bb40-def16be8bc55)

## POLICY ITERATION ALGORITHM
The algorithm implemented in the policy_iteration is a method used to find the optimal policy in a Markov decision process (MDP). Here's a step-by-step explanation of the algorithm:

1.Initialize the policy pi. In this implementation, a random action is chosen for each state s in the MDP P. The initial policy is represented by the lambda function pi=lambda s:{s:a for s,a in enumerate(random_actions)}[s], where random_actions is a list of randomly chosen actions for each state.

2.Enter a loop that continues until the policy pi is no longer changing. This is determined by comparing the previous policy (old_pi) with the current policy computed in the loop.

3.Store the previous policy as old_pi for comparison later.

4.Perform policy evaluation using the function policy_evaluation. This step calculates the state-values (V) for each state s given the current policy pi. The state-values represent the expected cumulative rewards starting from state s following policy pi and discounting future rewards by a factor of gamma. The function policy_evaluation is called with the arguments pi, P, gamma, and theta.

5.Perform policy improvement using the function policy_improvement. This step updates the policy pi based on the current state-values V. The function policy_improvement is called with the arguments V, P, and gamma.

6.Check if the policy has converged by comparing the previous policy old_pi with the current policy {s:pi(s) for s in range(len(P))}. If they are the same for all states s, the loop is exited.

7.Return the final state-values V and the optimal policy pi.

To summarize, policy iteration iteratively improves the policy by alternating between policy evaluation and policy improvement steps until convergence is reached. The algorithm guarantees to find the optimal policy for the given MDP P with a discount factor gamma



## POLICY IMPROVEMENT FUNCTION
The algorithm implemented in the policy_iteration is a method used to find the optimal policy in a Markov decision process (MDP). Here's a step-by-step explanation of the algorithm:

1.Initialize the policy pi. In this implementation, a random action is chosen for each state s in the MDP P. The initial policy is represented by the lambda function pi=lambda s:{s:a for s,a in enumerate(random_actions)}[s], where random_actions is a list of randomly chosen actions for each state.

2.Enter a loop that continues until the policy pi is no longer changing. This is determined by comparing the previous policy (old_pi) with the current policy computed in the loop.

3.Store the previous policy as old_pi for comparison later.

4.Perform policy evaluation using the function policy_evaluation. This step calculates the state-values (V) for each state s given the current policy pi. The state-values represent the expected cumulative rewards starting from state s following policy pi and discounting future rewards by a factor of gamma. The function policy_evaluation is called with the arguments pi, P, gamma, and theta.

5.Perform policy improvement using the function policy_improvement. This step updates the policy pi based on the current state-values V. The function policy_improvement is called with the arguments V, P, and gamma.

6.Check if the policy has converged by comparing the previous policy old_pi with the current policy {s:pi(s) for s in range(len(P))}. If they are the same for all states s, the loop is exited.

7.Return the final state-values V and the optimal policy pi.

To summarize, policy iteration iteratively improves the policy by alternating between policy evaluation and policy improvement steps until convergence is reached. The algorithm guarantees to find the optimal policy for the given MDP P with a discount factor gamma.

### PROGRAM:
```
Register No: 212222240099
Name: Siva Chandran R
```

```
def policy_improvement(V, P, gamma=1.0):
    Q = np.zeros((len(P), len(P[0])), dtype=np.float64)
    # Write your code here to implement policy improvement algorithm
    for s in range(len(P)):
      for a in range(len(P[s])):
        for prob, next_state,reward, done in P[s][a]:
          Q[s][a]+= prob*(reward+gamma*V[next_state]*(not done))
          new_pi = lambda s: {s:a for s, a in enumerate(np.argmax(Q, axis=1))}[s]

    return new_pi
```
## POLICY ITERATION FUNCTION
```
Register No: 212222240099
Name: Siva Chandran
```
```
def policy_iteration(P, gamma=1.0,theta=1e-10):
  random_actions=np.random.choice(tuple(P[0].keys()),len(P))
  pi = lambda s: {s:a for s, a in enumerate(random_actions)}[s]
  while True:
    old_pi = {s:pi(s) for s in range(len(P))}
    V = policy_evaluation(pi, P,gamma,theta)
    pi = policy_improvement(V,P,gamma)
    if old_pi == {s:pi(s) for s in range(len(P))}:
      break
  return V,pi
```
## OUTPUT:
### Optimal Policy 
![311115051-344579b2-416f-45b4-a760-febc26bd5765](https://github.com/obedotto/policy-iteration-algorithm/assets/113497395/61094ef3-23e4-44cd-8d0c-08ecac426522)

### Optimal Value Function:
![311115113-139579a7-c94a-45d1-8714-93741bc4061a](https://github.com/obedotto/policy-iteration-algorithm/assets/113497395/176efa10-9f7f-4a8c-a9ab-3a9dba01ad03)

### Success Rate for Optimal Policy:
![311115095-a88f4690-3e6d-418b-8f19-cb66d582f878](https://github.com/obedotto/policy-iteration-algorithm/assets/113497395/9ad27010-5a60-4f86-b8ad-7fc07c814a74)



## RESULT:
Thus, a program is developed to perform policy iteration for the given MDP.


