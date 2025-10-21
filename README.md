# Reinforcement Learning: Multi-Armed Bandits

A comprehensive implementation and analysis of Multi-Armed Bandit (MAB) algorithms for solving exploration-exploitation trade-offs in reinforcement learning.

## Overview

This project implements and compares various Multi-Armed Bandit algorithms across different environments, from simple deterministic bandits to complex non-stationary scenarios. The implementations include detailed performance analysis, visualizations, and practical recommendations for real-world applications.

## Algorithms Implemented

### Core Algorithms
- **Epsilon-Greedy**: Balances exploration and exploitation with a fixed probability parameter
- **Optimistic Initial Values (OIV)**: Encourages early exploration through optimistic Q-value initialization
- **Upper Confidence Bound (UCB)**: Uses uncertainty estimates to guide action selection
- **Constant Step-Size Tracking**: Adapts to non-stationary environments using exponential recency-weighted averaging

### Algorithm Variants Tested
- Epsilon-Greedy with multiple epsilon values (0.0, 0.01, 0.05, 0.1, 0.2, 0.3, 0.5)
- OIV with different initial values (Q₀ = 5, 10, 15)
- UCB with varying confidence levels (c = 0.5, 1.0, 2.0)
- Tracking algorithms with different learning rates (α) and exploration rates (ε)

## Experimental Environments

### 1. Deterministic Bandits
Fixed rewards across 5 bandits. Tests basic greedy strategy in known environments.

**Environment**: BanditEnv_1  
**Rewards**: [-10, 6, 8, 0, -2]  
**Strategy**: Simple greedy selection after initial exploration

### 2. Stochastic Bandits (Gaussian)
Rewards sampled from normal distributions with different means and standard deviations.

**Environment**: BanditEnv_2  
**Mean Rewards**: [-10, 6, 8, 0, -2]  
**Standard Deviation**: 1.0  
**Trials**: 200

### 3. Stochastic Bandits (Variable Variance)
Tests algorithm performance under different noise conditions.

**Configurations**:
- Low variance (σ = 1.0)
- High variance (σ = 5.0)

### 4. Non-Stationary Bandits
Bandit means change linearly over time, requiring continuous adaptation.

**Environment**: BanditEnv_3  
**Initial Means**: [-10, 6, 8, 0, -2]  
**Mean Changes per Trial**: [0.15, -0.1, -0.15, 0.05, 0.1]  
**Trials**: 200

### 5. Production Line (Bernoulli Bandits)
Real-world application simulating production line selection with binary outcomes.

**Environment**: ProductionLineBandit  
**Success Probabilities**: [0.5, 0.6, 0.55, 0.8]  
**Trials**: 500

## Key Results

### Stationary Environments
- **Epsilon-Greedy (ε=0.1)**: Achieves 1567.89 total reward (98.0% of optimal)
- **OIV (Q₀=15)**: Fastest convergence with minimal regret after initial exploration
- **UCB (c=2.0)**: Best performance in high-variance environments

### Non-Stationary Environments
- **Sample Averaging (ε=0.1)**: Surprisingly effective with 1394 total reward (76% of theoretical optimal)
- **Tracking (ε=0.2, α=0.3)**: Best constant step-size configuration with 1268 total reward
- **Traditional UCB/OIV**: Failed to adapt, achieving only ~1010 reward (72% regret)

### Production Line Application
- **OIV (Q₀=1.0)**: Winner with 392/400 reward and only 1.05 regret
- **Epsilon-Greedy (ε=0.1)**: 392 reward but 10.25 regret (10x more wasteful exploration)
- **UCB (c=1.0)**: 372 reward, 21.75 regret
- **Pure Greedy**: Catastrophic failure with 241 reward, 150 regret (62% loss)

## Features

### Comprehensive Analysis
- Cumulative reward tracking
- Regret analysis (cumulative and per-trial)
- Action distribution visualization
- Convergence analysis
- Parameter sensitivity studies
- Cross-algorithm comparisons

### Visualizations
Over 20 detailed plots including:
- Reward evolution over time
- Cumulative performance comparisons
- Action selection heatmaps
- Running average rewards
- Exploration vs exploitation patterns
- Q-value evolution
- UCB bonus analysis

### Statistical Rigor
- Multiple runs for statistical significance
- Mean and standard deviation reporting
- Confidence intervals
- Theoretical optimal comparisons

## Project Structure

```
Assignment 3/
├── Session_02_Multi_Armed_Bandits_Assignment.ipynb    # Main implementation notebook
└── README.md                                          # This file
```

## Requirements

- Python 3.x
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Jupyter Notebook

## Installation

```bash
# Clone the repository
git clone https://github.com/Iviwe01/Reinforcement-Learning-Multi-Armed-Bandits.git

# Navigate to the directory
cd Reinforcement-Learning-Multi-Armed-Bandits

# Install dependencies
pip install numpy pandas matplotlib seaborn jupyter
```

## Usage

```bash
# Launch Jupyter Notebook
jupyter notebook Session_02_Multi_Armed_Bandits_Assignment.ipynb
```

Run the cells sequentially to reproduce all experiments and visualizations.

## Key Insights

### When to Use Each Algorithm

**Epsilon-Greedy**
- Best for: Robust baseline performance across various environments
- Optimal when: Need simple, interpretable exploration strategy
- Parameter guidance: ε=0.1 for most applications, ε=0.05 for low-noise environments

**Optimistic Initial Values**
- Best for: Stationary environments with clear winners
- Optimal when: Early convergence is critical, exploration cost is uniform
- Parameter guidance: Q₀ should be higher than maximum expected reward

**Upper Confidence Bound**
- Best for: High-variance Gaussian environments
- Optimal when: Theoretical guarantees are needed, variance is unknown
- Parameter guidance: c=2.0 for exploration, c=1.0 for balanced performance

**Constant Step-Size (Tracking)**
- Best for: Non-stationary environments
- Optimal when: Reward distributions change over time
- Parameter guidance: α=0.2-0.3 for moderate changes, higher for rapid drift

### Critical Findings

1. **Pure greedy fails catastrophically** in stochastic environments (62% regret in production line)
2. **Sample averaging surprisingly effective** in non-stationary settings (beats UCB and OIV)
3. **OIV dominates in Bernoulli bandits** with minimal regret through front-loaded exploration
4. **Convergent algorithms fail** when environments are non-stationary
5. **Exploration rate matters**: 5x regret difference between ε=0.1 and ε=0.5

## Academic Context

This project was completed as part of the Reinforcement Learning course at Howest University. It demonstrates fundamental concepts in:
- Exploration-exploitation trade-offs
- Online learning algorithms
- Sequential decision making
- Adaptive strategies for changing environments

## License

This project is available for educational purposes.

## Author

Iviwe Mtambeka 
Howest University  
Reinforcement Learning Course - 2025

## References

- Sutton, R. S., & Barto, A. G. (2018). Reinforcement Learning: An Introduction (2nd ed.)
- Auer, P., Cesa-Bianchi, N., & Fischer, P. (2002). Finite-time Analysis of the Multiarmed Bandit Problem
- Vermorel, J., & Mohri, M. (2005). Multi-armed Bandit Algorithms and Empirical Evaluation
