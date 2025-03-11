# Quantum computing and option pricing project



## About

The goal of this project is to design a quantum circuit that leverages the Quantum Amplitude Estimation algorithm to approximate the price of a call option. More precisely, given a call option with strike $K$ and maturity $T$ on an underlying $S$ with volatility $\sigma$, the goal of this project is to design a circuit that constructs a state of the form
$$\sqrt{1-a}\left(|\Psi_0\rangle_n \otimes |1\rangle\right) + \sqrt{a}\left(|\Psi_1\rangle_n \otimes |1\rangle\right)$$
such that $a$ is an approximation of $\mathbb{E}\left[(S_T - K)_+\right]$. The Quantum Estimation Algorithm is then used to estimate the value of $a$, which represents the *compounded* price of the call option.

## Work to be done

At the end of the project, each group should produce a Jupyter notebook that contains the code that was produced, along with an analysis of the advantages and limits of using a quantum algorithm to price financial derivatives.

The [provided](Source/quantum_pricing.ipynb) notebook can be used as a guideline to carry out the project.

## Technical environment

The quantum algorithms will be programmed with Qiskit. It is **strongly** recommended to take a look at the [Basics of Quantum Information](https://learning.quantum.ibm.com/course/basics-of-quantum-information/) course before starting the project, especially the parts involving Qiskit.