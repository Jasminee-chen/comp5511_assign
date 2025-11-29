### comp5511 assignment2
### Task4:REINFORCEMENT LEARNING FOR GAME
This project aims to apply the Q-Learning algorithm to solve the FrozenLake-v1 game in the Gymnasium environment, specifically the navigation problem on an 8x8 grid. The core objective is to compare the learning performance of the agent in deterministic and stochastic environments.

### 1. Task Goal

Implement the Q-Learning algorithm to train the agent to navigate in the 8x8 FrozenLake environment,
from the starting point (0, 0) to the ending point (7, 7).

Compare the performance difference between deterministic environments (is_slippery=False) and stochastic environments (is_slippery=True).

Analyze the impact of key hyperparameters ($\alpha, \gamma, \epsilon$) on the learning process.
### 2. 
- Python 3.8+：Core programming language

- NumPy 1.26.0：Used for creating Q-Tables and numerical computation

- Gymnasium：0.29.1：Provides the FrozenLake-v1 game environment

- Matplotlib 3.7.2：Plots learning curves (total reward vs. number of rounds)

- Imageio 2.31.1：Used to generate GIFs or animations of agent policy execution
