# Infotaxis Search and Performance Benchmark

This project implements and visualizes **Infotaxis**, a biologically inspired strategy for localizing an unknown signal-emitting source (here we use the example of a gas leak) using information theory. Infotaxis is an information-theoretic search strategy designed to locate a hidden source (e.g., odor, gas, or radiation) in environments where signals are sparse, noisy, or intermittent. It models the problem as a Partially Observable Markov Decision Process (POMDP) and balances exploration (gathering information) and exploitation (moving toward likely source locations) using the expected reduction in Shannon entropy.Attached in this file
is a report that discusses the methodology of infotaxis and possible applications of them, as well as a simple code example illustrating how infotaxis works. 
 
<p align="center">
  <img src="https://github.com/user-attachments/assets/c9bdf184-c837-437b-8e17-568aa012d18e" alt="Odor Leak Simulation" width="400"/>
</p>
<p align="center"><sub><i>Figure 1. Simulated odor leak scenario where the searcher navigates a 2D grid to localize the source based on intermittent sensor signals.</i></sub></p>


Below is a simple summary of the math showing how infotaxis works. 

### Belief Representation
At each timestep \( t \), the agent maintains a **belief distribution** over possible source locations:

$$
P_t(x_s, y_s)
$$

---

### Bayesian Belief Update
After observing a signal \( Z_t \in \{0, 1\} \) (signal or no signal), the belief is updated using Bayes' rule:

$$
P_{t+1}(x_s, y_s) = \frac{P(Z_t \mid x_t, y_t, x_s, y_s) \cdot P_t(x_s, y_s)}{\sum_{x', y'} P(Z_t \mid x_t, y_t, x', y') \cdot P_t(x', y')}
$$

Where:
- \( (x_t, y_t) \): current position of the searcher.
- \( (x_s, y_s) \): hypothesized source location.

The likelihood (sensor model) is often modeled as exponential decay with distance:

$$
P(Z_t = 1 \mid x_t, y_t, x_s, y_s) = \exp\left(-\frac{d(x_t, y_t, x_s, y_s)}{\lambda}\right)
$$


### 📉 Entropy Computation
The Shannon entropy of the belief distribution is:

$$
S(P_t) = -\sum_{x_s, y_s} P_t(x_s, y_s) \log P_t(x_s, y_s)
$$

Entropy measures uncertainty: lower entropy means higher confidence in the source location.

### Action Selection: Maximizing Information Gain
For each possible move \( a \), infotaxis evaluates the expected entropy **after** making that move:

$$
\mathbb{E}[S(P_{t+1}) \mid a] = \sum_{Z_t \in \{0, 1\}} P(Z_t \mid a) \cdot S(P_{t+1} \mid Z_t, a)
$$

The agent selects the move that maximizes expected **entropy reduction**:

$$
a^* = \arg\max_a \left[ S(P_t) - \mathbb{E}[S(P_{t+1}) \mid a] \right]
$$

---

###  Markovian Process
Infotaxis operates as a **first-order Markov process**:
- The next state (belief) depends only on the current state and observation.
- No history beyond \( P_t \) is required.

- Finds that DRL can **learn better policies than infotaxis**, especially in 2D environments.
- In higher dimensions, the gap between Infotaxis and DRL closes.
- Infotaxis performs particularly well when signal emissions are sparse or noisy.

- Infotaxis is reliable, robust, and biologically plausible.
- DRL-based strategies outperform infotaxis in **average search time**.
- The paper provides a **baseline for benchmarking search algorithms** in environments with partial observability and stochastic measurements.

## Features of This Repo (Codebase)
-  2D infotaxis simulation using Bayesian belief updates.
-  Entropy-driven movement strategy.
-  Searcher trajectory tracking.
-  Sensor hit/miss simulation.
-  Easily pluggable model for DRL, MCTS, or greedy alternatives.

To extend the infotaxis framework as proposed in the paper, you can model the search problem as a Partially Observable Markov Decision Process (POMDP) and apply advanced planning or learning techniques.
One approach is to implement Deep Reinforcement Learning (DRL) methods, such as PPO or DQN, which allow the searcher to learn optimal policies directly from simulated experience, often outperforming infotaxis
in average search time. Another option is to use Monte Carlo Tree Search (MCTS) to simulate multiple future action paths and select moves that maximize long-term information gain.
Finally, you can replace the entropy-based move selector with a neural network policy trained to approximate optimal decisions under uncertainty. These extensions provide more flexible and potentially more
efficient strategies for source localization in complex or high-dimensional environments.










Loisy, A., & Eloy, C. (2022). "Searching for a source without gradients: how good is infotaxis and how to beat it." 
Proceedings of the Royal Society A. 
DOI: https://doi.org/10.1098/rspa.2022.0118
