# **Finite-Horizon Dynamic Programming and Simulation**

## Project Overview

This repository contains the full solution to the **Week 1 assignment** of the *Dynamic Programming & Reinforcement Learning* course.
The task explores **finite-horizon stochastic dynamic programming** applied to a simplified **inventory management** problem with random demand and unreliable supply.

We:

* Define a **state–action formulation** of the system,
* Solve it by **backward induction (Bellman recursion)**,
* Derive the **optimal policy** π*(t, x),
* Validate it through **1 000 Monte Carlo simulations**, and
* Compare the simulated rewards with the theoretical DP expectation.

The full mathematical derivation and interpretation are provided in [`assignment_report.pdf`](assignment_report.pdf),
and all code used for computation and visualization is available in [`dprl-w1-script.ipynb`](dprl-w1-script.ipynb).

## Key Results

| Quantity                             | Symbol | Value       |
| ------------------------------------ | ------ | ----------- |
| Expected maximal reward (DP)         | V₁(5)  | **≈ 32.37** |
| Mean reward (simulation, 1 000 runs) |        | **≈ 32.35** |

These nearly identical values confirm that the simulated process reproduces the theoretical optimum and that the implemented policy performs as expected under uncertainty.

<img width="1920" height="1440" alt="optimal_policy" src="https://github.com/user-attachments/assets/dd1b7d81-778b-4c5c-9890-95a66a2a2c3f" />

<img width="1920" height="1440" alt="reward_histogram" src="https://github.com/user-attachments/assets/ed914d04-1743-4334-96df-46a074b2eaff" />

## Model Summary

The system evolves over **T = 150** discrete periods.

* **State (xₜ):** current inventory
* **Action (aₜ):** {0 = no order, 1 = order one unit}
* **Demand (Dₜ):** Bernoulli (pₜ) with pₜ = (t−1)/149 (increasing demand probability)
* **Order arrival (Aₜ):** Bernoulli (0.5) when aₜ = 1
* **Reward:** sales revenue ( +1 per item ) − holding cost ( 0.1 × inventory )

The Bellman recursion:
[
V_t(x) = -0.1x + \max_a \mathbb{E}[,\text{profit}(x,a), + V_{t+1}(x'),],
]
was solved by backward induction to obtain V and π* over all (t, x).

## Broader Interpretation – *From Inventory to Finance*

Although the task is presented in an operations-research context, its mathematical skeleton mirrors many **financial optimization** problems:

| Inventory Problem Concept | Financial Analogue                                |
| ------------------------- | ------------------------------------------------- |
| Inventory level           | Cash buffer or risky-asset position               |
| Ordering decision         | Trade / rebalancing / hedging action              |
| Uncertain delivery        | Execution risk or market liquidity uncertainty    |
| Random demand             | Random cash outflow or market shock               |
| Holding cost              | Opportunity cost, financing rate, or risk penalty |
| Finite horizon            | Investment horizon or regulatory reporting period |

Under this lens, the same DP structure could support:

* **Liquidity-buffer optimization:** deciding when to raise or deploy cash given uncertain outflows.
* **Dynamic risk management:** adjusting exposure to maintain capital adequacy under stochastic losses.
* **Optimal trading & execution:** planning orders when execution probability varies (analogous to our 0.5 arrival rate).
* **Portfolio rebalancing:** balancing expected return (sales revenue) against risk or transaction costs (holding cost).

Thus, even a simple DP exercise forms the computational foundation for **dynamic asset-allocation**, **stochastic control**, and **reinforcement-learning approaches** in quantitative finance.

## Takeaway

This project demonstrates how **dynamic programming** translates theoretical stochastic control principles into quantifiable, testable strategies.
Whether the “inventory” represents *physical goods* or *financial exposure*, the same Bellman logic applies:

*Decide today, while thinking about tomorrow’s uncertainty.*
