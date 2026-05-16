# Frozen Lake - Reinforcement Learning Project

A comprehensive implementation and comparison of three reinforcement learning algorithms solving the **Frozen Lake** environment from OpenAI Gymnasium.

**Repository**: https://github.com/Ritupriya176/Frozen-Lake

## Project Overview

This project demonstrates how different RL algorithms learn to navigate a slippery 4x4 frozen lake grid from start (S) to goal (G) while avoiding holes. Each agent learns through interaction with the environment and optimizes its policy to maximize success rate.

## Environment

- **Environment**: Frozen Lake-v1 (4x4 grid)
- **State Space**: 16 states (0-15)
- **Action Space**: 4 actions (Left, Down, Right, Up)
- **Slippery Surface**: True (random movements with 1/3 probability)
- **Training Episodes**: 5000
- **Evaluation Episodes**: 1000

## Algorithms Implemented

### 1. Q-Learning
- **Type**: Off-policy, value-based algorithm
- **Learning Rate**: 0.8
- **Discount Factor**: 0.99
- **Success Rate**: **69.40%**
- **Description**: Updates Q-values based on the maximum Q-value of the next state, regardless of the action actually taken.

**Key Features**:
- Epsilon-greedy exploration (decay from 1.0 to 0.01)
- Reward shaping (5.0 for reaching goal, -0.5 for falling)
- Learning rate decay over episodes

### 2. SARSA (State-Action-Reward-State-Action)
- **Type**: On-policy, temporal difference learning
- **Learning Rate**: 0.1
- **Discount Factor**: 0.99
- **Success Rate**: **29.20%**
- **Description**: Updates Q-values based on the actual action taken in the next state, making it more conservative.

**Key Features**:
- More cautious learning approach
- Considers real actions taken, not optimal ones
- Slower convergence but more stable in some scenarios

### 3. Deep Q-Network (DQN) ⭐
- **Type**: Off-policy, deep reinforcement learning
- **Network Architecture**: 3-layer fully connected neural network
- **Hidden Layers**: 64 units each
- **Success Rate**: **79.00%** (Best Performer)
- **Description**: Uses a neural network to approximate Q-values with experience replay and target networks.

**Key Features**:
- Experience replay buffer (capacity: 10,000)
- Target network updated every 10 episodes
- Adam optimizer (lr=0.001)
- Reward shaping (5.0 for goal, -1.0 for hole)
- One-hot state encoding

## Results Comparison

| Algorithm | Success Rate | Method |
|-----------|-------------|--------|
| Q-Learning | 69.40% | Tabular, Off-policy |
| SARSA | 29.20% | Tabular, On-policy |
| **DQN** | **79.00%** | Neural Network, Off-policy |

## Performance Metrics

Each algorithm tracks:
- **Success Rate**: Percentage of episodes ending at the goal
- **Cumulative Rewards**: Rolling average over 100 episodes
- **Episode Rewards**: Individual episode performance
- **Value Functions**: Learned state values visualized as heatmaps
- **Policies**: Optimal action per state visualization

## Installation & Usage

### Requirements
```bash
pip install gymnasium numpy matplotlib torch
```

### Running the Project
```python
# The project is implemented in Jupyter Notebook format
# Open RL_PROJECT.ipynb in Google Colab or Jupyter

# Train Q-Learning agent (Cell 1)
# Train SARSA agent (Cell 2)
# Train DQN agent (Cell 3)
```

## Output Files

- `frozen_lake4x4.pkl` - Trained Q-Learning policy
- `frozen_lake4x4_sarsa.pkl` - Trained SARSA policy
- `frozen_lake_dqn.pth` - Trained DQN neural network weights
- `frozen_lake4x4_metrics.png` - Performance visualization
- `frozen_lake4x4_value_function.png` - Q-Learning value heatmap
- `frozen_lake4x4_sarsa_policy.png` - SARSA policy visualization
- `frozen_lake_dqn_value_function.png` - DQN value heatmap

## Key Insights

1. **DQN Superiority**: Deep Q-Network achieves the best performance (79%) due to:
   - Function approximation with neural networks
   - Experience replay for stable learning
   - Target network preventing divergence

2. **Q-Learning Performance**: Solid baseline (69.4%) with simpler tabular approach
   - Fast to train
   - Easy to interpret
   - Sufficient for small state spaces

3. **SARSA Limitations**: Lowest performance (29.2%) because:
   - On-policy learning is conservative
   - Slippery surface makes actual actions unreliable
   - Slower convergence on stochastic environments

## Hyperparameter Tuning

### Q-Learning
- Learning Rate: 0.8 → 0.1 (decay)
- Epsilon: 1.0 → 0.01 (decay: 0.9995)

### SARSA
- Learning Rate: 0.1 → 0.01 (decay)
- Epsilon: 1.0 → 0.01 (decay: 0.9995)

### DQN
- Learning Rate: 0.001 (Adam optimizer)
- Epsilon: 1.0 → 0.01 (decay: 0.995)
- Batch Size: 64
- Target Update Frequency: Every 10 episodes

## Future Improvements

- Implement Double DQN for reduced overestimation
- Add Dueling DQN architecture
- Try Policy Gradient methods (A3C, PPO)
- Visualize learning progress with animations
- Test on larger Frozen Lake variants (8x8)

## References

- Sutton & Barto - Reinforcement Learning: An Introduction
- OpenAI Gymnasium Documentation
- Deep Reinforcement Learning Papers

## License

MIT License - Feel free to use for educational purposes

## Author

[Ritupriya176](https://github.com/Ritupriya176)

---

**Last Updated**: May 16, 2026
