# Project 3: Collaboration and Competition - Report

### Learning Algorithm

Basically I used [DDPG(Deep Deterministic Policy Gradients) in ddpg-pendulum from Udacity DRLND Repo](<https://github.com/udacity/deep-reinforcement-learning/tree/master/ddpg-pendulum>). Because DDPG can be used for continous action, it compensates for the disadvantages of DQN.
DDPG uses two pairs of networks, Actor and Critic. *The Actor-Critic learning algorithm is used to represent the policy function independently of the value function. The policy function structure is known as the actor, and the value function structure is referred to as the critic.* (from [link](<https://pemami4911.github.io/blog/2016/08/21/ddpg-rl.html>))
Each pair consists of a Regular network and a Target network, like DQN. DQN is updated at regular time steps from regular network to target network at one time, but DDPG updates little by 0.01% in a way called soft update.

And I used 2 agents at the same time. At first I used just one agent, and reward never got over +0.1 for 4,000 episodes. And then I seperate 2 agents and also replay buffer. I didn't use replay buffer sharing, but it worked anyway.

### Hyperparameters

I tried 10,000 to 100,000 on buffer size, 64 to 512 on batch size, 0.95 to 0.99 to gamma, 0.001 to 0.0001 on actor learning rate, 0.001 to 0.0001 to critic learning rate, 1 to 20 on learn step, 10 to 20 on learn count. Best result is below.

* Buffer size : 100,000
* Batch size : 512
* Gamma : 0.99
* Tau(for soft update) : 0.001
* Actor learning rate : 0.0001
* Critic learning rate : 0.0003
* Learn step(update per this step) : 4
* Learn count(on one step) : 10
* Agent count(each player) : 1


### Plot of Rewards

Compared to project2, I had the basic code, so I was able to complete the task quickly. At first I tried to learn with one agent, then I used two agents. The replay buffer was not shared. It is strange that the average score has decreased as time passed since it exceeded +0.5 in a short time. Anyway, the average of 100 episodes exceeded +0.5 and the work was completed normally.

![](<graph.png>)


### Future Work

* Sharing Replay Buffer : If two agents share the replay buffer, the amount of memory they occupy will be reduced. Since it is possible to invest in other hyperparameters by the amount of memory that is reduced (cf. BATCH_SIZE), this is thought to indirectly increase learning efficiency.

* [Hyperparameter optimization](<https://en.wikipedia.org/wiki/Hyperparameter_optimization>) : Some Hyperparameter is more stable than others. There are many hyperparameters in machine learning, so we should find good enough but save our time. There are some search algorithms for these work - grid search, random search, bayesian optimization, gradient-based optimization, evolutionary optimization, and so on.

* [add parametric noise](<https://blog.openai.com/better-exploration-with-parameter-noise/>) : According to Deepmind, adding adaptive noise to the parameters of reinforcement learning algorithms frequently boosts performance. In this code I just added action noise but not parametric noise.
