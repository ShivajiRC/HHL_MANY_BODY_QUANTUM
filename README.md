# HHL_MANY_BODY_QUANTUM
# Adapting the HHL Algorithm to Quantum Many-Body Theory

An implementation and benchmarking study of HHLite and AdaptHHLite,
resource-efficient variants of the Harrow-Hassidim-Lloyd (HHL)
algorithm for linear systems arising in quantum many-body theory.

## Overview

The HHL algorithm provides a quantum approach to solving linear systems

$$
A x = b.
$$

In the linearized coupled-cluster formulation of quantum chemistry,
the cluster amplitudes can be obtained from a linear system of this form,
with the resulting solution used to estimate the correlation energy.

This project implements the standard HHL algorithm and two
resource-efficient modifications:

- **HHLite:** reduces circuit depth by fixing eigenvalue bits that are
  strongly biased in the quantum phase estimation output.
- **AdaptHHLite:** combines the Lite procedure with matrix scaling to
  simplify the controlled rotations.

## Systems

The implementations are tested on linear systems corresponding to:

- H₂
- LiH

## Benchmarking

The circuits are evaluated under three computational settings:

- Noiseless simulation
- Noisy simulation with a depolarizing noise model
- IBM quantum hardware

Circuit depth and correlation-energy error are used to evaluate the
trade-off between resource reduction and accuracy.

## Results

For the H₂ system, AdaptHHLite reduces the transpiled circuit depth from

$$
101 \rightarrow 52 \rightarrow 27 \rightarrow 14 \rightarrow 7,
$$

corresponding to approximately 93% depth compression at four fixed
qubits, while maintaining an energy error below 2%.

Further fixing can lead to a loss of valid measurement outcomes and
failure of the estimation procedure.

![AdaptHHLite results](figures/adapthhlite_results.png)

## Contents

- `notebooks/` — implementation and numerical experiments
- `figures/` — generated performance plots
- `report/` — project report

## Requirements

- Python
- NumPy
- SciPy
- Matplotlib
- Qiskit
- Qiskit Aer
- Qiskit IBM Runtime

## Reference

N. Baskaran et al.,
*Adapting the HHL Algorithm to Quantum Many-Body Theory*,
Physical Review Research **5**, 043113 (2023).
