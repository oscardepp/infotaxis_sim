# Infotaxis Search and Performance Benchmark

This project implements and visualizes **Infotaxis**, a biologically inspired strategy for localizing an unknown signal-emitting source (here we use the example of a gas leak) using information theory. Attached in this file
is a report that discusses the methodology of infotaxis and possible applications of them, as well as a simple code example illustrating how infotaxis works. 
Evaluates **Infotaxis** performance across 1D to 4D search problems.
- Models the source-tracking problem as a **Partially Observable Markov Decision Process (POMDP)**.
- Shows that Infotaxis is:
    - Robust
    - Near-optimal in many scenarios
    - Simple to implement
<p align="center">
  <img src="https://github.com/user-attachments/assets/c9bdf184-c837-437b-8e17-568aa012d18e" alt="Odor Leak Simulation" width="400"/>
</p>
<p align="center"><sub><i>Figure: Simulated odor leak scenario where the searcher navigates a 2D grid to localize the source based on intermittent sensor signals.</i></sub></p>

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
