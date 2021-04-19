
### 1. Introduction
The goal  of project is train 2 agents in Unity environment to play tennis, two agents use rackets to bounce the ball over a net. if agent hit the ball, a reward of +0.1. If agent make the ball hit ground or out of the bounce, it recieve a reward of -0.01. So, purpose of the game to kepp the ball play.

The task is episodic, and in order to solve the environment, the agents must get an average score of +0.5 (over 100 consecutive episodes, after taking the maximum over both agents).

The environment is considered solved, when the average (over 100 episodes) of those scores is at least +0.5.

### 2. DDPG Algorithm

![image](https://user-images.githubusercontent.com/31414852/115268320-26efeb80-a108-11eb-9157-6ae5a1a51af4.png)

We use DDPG algorithm to train,an Actor-Critic method.
The observation space is included of 8 variables with the position, velocity of the ball and racket, the environment returns 3 stacked observation spaces at each timestep, so the returned variable has 24 dimensions.

We use same Actor and Critic networks for both agents, and 2 Neural Networks. One to estimate the best action for a particular state, and another one to estimate the Value Function.

We add the experiences of both the players to the same replay buffer and sample from it to compute the loss. All steps (State, Action, Reward, Next State)  tuples  from each one of the rackets are saved in to a queue in memory.

Adam optimizer with an actor learning rate of 0.001, critic learning rate of 0.001,batch size of 128, discount factor of 0.99.

### 3. Results
#### Selected Hyper-parameters

The code uses the following Hyper-parameters:

- *`Number of Hidden Layers`*  =  2
- *`Neurons in 1° layer`*  =  128
- *`Neurons in 2° layer`*  =  128
- *`Gamma`*  =  0.99
- *`TAU`*  =  1e-3
- *`Actor LR`*  =  1e-3
- *`Critic LR`*  =  1e-3
- *`Batch Size`*  =  128

---

![image](https://user-images.githubusercontent.com/31414852/115264247-205f7500-a104-11eb-8444-c0943e0869e2.png)

![image](https://user-images.githubusercontent.com/31414852/115264271-26555600-a104-11eb-80f5-4abd16452c0b.png)

The training is terminated when the average reward per episode reaches 0.5. We were able to solve the environement in 1616 episodes.
### 4. Future Work
We trained a the environment using DDPG algorithm. In future we can explore other algorithms like MADDPG.
We can also tune the hyperparameters further to solve the environment in fewer number of episodes. 
