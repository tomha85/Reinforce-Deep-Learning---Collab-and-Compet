
### Introduction

Environment solved criterion: The task is episodic, and in order to solve the environment, the agents must get an average score of +0.5 (over 100 consecutive episodes, after taking the maximum over both agents). Specifically,

After each episode, we add up the rewards that each agent received (without discounting), to get a score for each agent. This yields 2 (potentially different) scores. We then take the maximum of these 2 scores.
This yields a single score for each episode.
The environment is considered solved, when the average (over 100 episodes) of those scores is at least +0.5.

### 2. Learning Algorithm
We train the network using DDPG algorithm. For the Actor, we use a three layer MLP with 128 and 128 neurons respectively in hidden layers. The state vector is the 8 dimensional vector described in section 1. The output vector is of size 2. We use same Actor and Critic networks for both the players. We add the experiences of both the players to the same replay buffer and sample from it to compute the loss.
We train the network using Adam optimizer with an actor learning rate of 0.001, critic learning rate of 0.001 and batch size of 128. We use a discount factor of 0.99.

### 3. Results
#### Selected Hyper-parameters

The code uses the following Hyper-parameters:

- **`Number of Hidden Layers`**  =  2
- **`Neurons in 1° layer`**  =  128
- **`Neurons in 2° layer`**  =  128
- **`Gamma`**  =  0.99
- **`TAU`**  =  1e-3
- **`Actor Learning Rate`**  =  1e-3
- **`Critic Learning Rate`**  =  1e-3
- **`Batch Size`**  =  128

---
The figure below shows average rewards per episode as the agent is being trained. The training is terminated when the average reward per episode reaches 0.5. We were able to solve the environement in 2052 episodes.

![image](https://user-images.githubusercontent.com/31414852/115264247-205f7500-a104-11eb-8444-c0943e0869e2.png)

![image](https://user-images.githubusercontent.com/31414852/115264271-26555600-a104-11eb-80f5-4abd16452c0b.png)

### 4. Future Work
We trained a the environment using DDPG algorithm. In future we can explore other algorithms like MADDPG.
We can also tune the hyperparameters further to solve the environment in fewer number of episodes. 
