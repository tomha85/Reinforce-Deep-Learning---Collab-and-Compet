
### 1. Introduction
The goal  of project is train 2 agents in Unity environment to play tennis, two agents use rackets to bounce the ball over a net. if agent hit the ball, a reward of +0.1. If agent make the ball hit ground or out of the bounce, it recieve a reward of -0.01. So, purpose of the game to keep the ball play as much as posssible.

The task is episodic, and in order to solve the environment, the agents must get an average score of +0.5 (over 100 consecutive episodes, after taking the maximum over both agents).

The environment is considered solved, when the average (over 100 episodes) of those scores is at least +0.5.

### 2. MADDPG Algorithm

![image](https://user-images.githubusercontent.com/31414852/115268320-26efeb80-a108-11eb-9157-6ae5a1a51af4.png)

We use DDPG algorithm to train, an Actor-Critic method. Multi-agent DDPG class uses 2 DDPG agents. MADDPG combines states, actions,rewards,dones from both agents and adds them to shared ReplayBuffer.

![image](https://user-images.githubusercontent.com/31414852/115271074-f2c9fa00-a10a-11eb-978b-c2b3cdd7698c.png)

The observation is included of 8 variables with the position, velocity of the ball and racket, the environment gets 3 stacked observation at each timestep, so the returned variable has 24 dimensions. We add the experiences of both the agents to the same replay buffer and sample them to compute the loss. All steps (State, Action, Reward, Next State)  tuples  from each one of the rackets are saved in to a queue in memory.

We use same Actor and Critic networks for both agents, and 2 neural networks. One network used to estimate the action for a state, and another is to estimate the value function Q(s,a).

Adam optimizer with an actor learning rate of 0.001, critic learning rate of 0.001,batch size of 128, discount factor of 0.99.

### 3. Results
#### Selected Hyper-parameters

The code uses parameters:
- **`Batch Size`**  =  128
- **`Number of Hidden Layers`**  =  2
- **`1st layer`**  =  128 
- **`2nd layer`**  =  128 
- **`GAMMA`**  =  0.99
- **`TAU`**  =  1e-3
- **`Actor LR`**  =  0.001
- **`Critic LR`**  =  0.001
- **`Weight_decay`**  =  0

---

![image](https://user-images.githubusercontent.com/31414852/115264247-205f7500-a104-11eb-8444-c0943e0869e2.png)

![image](https://user-images.githubusercontent.com/31414852/115264271-26555600-a104-11eb-80f5-4abd16452c0b.png)

The training is stopped at 1616 episodes and average rewards is more than 0.5. We can solve the environement in 1616 episodes.

### 4. Future Work
Adjust parameters affect the way of training. So we continue to get best parameters to get good performance of the game.
We also try anothe method and algorithms like multi-agent PPO or multi-agent DQN
