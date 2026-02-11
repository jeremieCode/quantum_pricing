# Quantum Option Pricing with Qiskit

## Project Overview

This project implements a quantum algorithm to estimate the price of a European Call Option using **Quantum Amplitude Estimation (QAE)**. By leveraging the principles of quantum superposition and interference, this approach offers a quadratic speedup over classical Monte Carlo simulations.

The core objective is to construct a quantum circuit that encodes the expected payoff of the option into the amplitude of a specific quantum state, and then estimate this amplitude.

## Mathematical Framework

The price of the call option is given by the discounted expectation of the payoff:
$ C = e^{-rT} \mathbb{E}\left[ \max(S_T - K, 0) \right] $

Where:
*   $S_T$: Spot price at maturity $T$ (following a log-normal distribution).
*   $K$: Strike price.
*   $r$: Risk-free interest rate.

## Implementation Details

The project is built using **Qiskit** and follows a modular quantum circuit design:

1.  **Probability Loading**: 
    - Discretization of the log-normal distribution of asset prices onto $n$ qubits.
    - Implementation of a loading operator $ \mathcal{P} $ using controlled-Ry rotations derived from the Grover-Rudolph algorithm.

2.  **Quantum Comparator**:
    - A digital logic circuit that flips an ancilla qubit if $ S_T \geq K $.
    - Uses 2's complement arithmetic and quantum carry logic.

3.  **Linear Payoff Encoding**:
    - Conditional rotation of an ancilla qubit to encode the linear function $ f(x) \approx S_T - K $.
    - The payoff is encoded such that the probability of measuring $ |1\rangle $ is proportional to the option price.

4.  **Amplitude Estimation**:
    - Usage of **Iterative Quantum Amplitude Estimation (IQAE)** to estimate the probability without the expensive Quantum Phase Estimation (QPE) controlled rotations.

## Repository Structure

*   `quantum_pricing.ipynb`: The main Jupyter Notebook containing the full implementation, tests for each module (comparator, piecewise linear function), and the final pricing simulation.
*   `requirements.txt`: List of Python dependencies required to run the project.
*   `README.md`: Project documentation.

## Requirements

To run this project, ensure you have Python installed. You can install the required dependencies using the following command:

```bash
pip install -r requirements.txt
```

This will install:
*   `qiskit`
*   `qiskit-aer`
*   `qiskit-algorithms`
*   `numpy`, `scipy`, `matplotlib`
*   `pylatexenc` (for circuit visualization)

## Usage

1.  Open the notebook `quantum_pricing.ipynb`.
2.  Configure the option parameters in the setup cells:
    ```python
    sigma = 0.2  # Volatility
    r = 0.05     # Risk-free rate
    T = 1.0      # Maturity
    S0 = 2.0     # Initial Spot Price
    K = 2.0      # Strike Price
    ```
3.  Run all cells to generate the quantum circuit and perform the estimation.
4.  Compare the Quantum result (`res`) with the classical Black-Scholes analytical value (`bs`).

## References

*   *Quantum Risk Analysis*, Woerner, S., & Egger, D. J. (2019).
*   *Option Pricing using Quantum Computers*, Stamatopoulos et al. (2020).
*   Qiskit Finance Tutorials.
