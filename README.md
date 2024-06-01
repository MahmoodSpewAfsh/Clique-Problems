# Clique and Largest Clique Problem Using Quantum Annealing
## Overview

This repository contains a Python implementation for solving the Clique Decision Problem using quantum annealing on the D-Wave quantum computer and finding the largest clique in a given graph using D-Wave's Quantum Annealer. A clique in a graph is a subset of vertices such that every two distinct vertices are adjacent. The largest clique problem, an NP-hard problem, involves finding the maximum complete subgraph within a given graph.

## Problem Description

### The Clique Decision Problem

The Clique Decision Problem is a fundamental problem in graph theory and computer science. Given an undirected graph \( G = (V, E) \) and an integer \( k \), the problem is to determine whether there exists a subset of \( k \) vertices that form a complete subgraph (clique) in \( G \).

### Formulating the Problem as a QUBO

Quantum Annealing (QA) and the D-Wave system can solve problems expressed in the Quadratic Unconstrained Binary Optimization (QUBO) form. The Clique Decision Problem can be formulated as a QUBO by encoding the constraints and objectives as binary variables:

1. **Binary Variables**: Define a binary variable \( x_{i,j} \) for each vertex \( v_i \) and each position \( j \) in the clique, where \( x_{i,j} = 1 \) if vertex \( v_i \) is in position \( j \) in the clique and \( x_{i,j} = 0 \) otherwise.

2. **Objective Function**: The QUBO objective function \( Q \) is constructed to enforce two conditions:
   - Exactly \( k \) vertices are selected.
   - The selected vertices form a clique.

The QUBO objective function is expressed as:
$$\[ Q(x) = A \sum_{i} (1 - \sum_{j} x_{i,j})^2 + B \sum_{i < j} \sum_{l} x_{i,l} x_{j,l} (1 - A_{ij}) \]$$
where \( A \) and \( B \) are large positive constants, and \( A_{ij} \) is the adjacency matrix of the graph \( G \).

### Definition of largest clique problem
A **clique** in an undirected graph \( G = (V, E) \) is a subset of vertices such that every two distinct vertices are connected by an edge. The **largest clique** is the clique of maximum size in the graph.

### Quantum Annealing Approach

Quantum annealing is a method used to find the global minimum of a given objective function over a given set of candidate solutions. It is particularly useful for solving combinatorial optimization problems such as the largest clique problem.

### Hamiltonian Formulation
To solve the largest clique problem using quantum annealing, we formulate it as a QUBO (Quadratic Unconstrained Binary Optimization) problem. The problem can be encoded into a Hamiltonian, where the ground state (minimum energy state) corresponds to the largest clique. The Hamiltonian is composed of three parts:

1. **Hamiltonian \( H_A \)**: Ensures the number of selected vertices matches the desired clique size.
2. **Hamiltonian \( H_B \)**: Ensures the selected vertices form a complete subgraph.
3. **Hamiltonian \( H_C \)**: Maximizes the number of selected vertices to find the largest clique.

### Hamiltonian Equations

1. **Hamiltonian \( H_A \)**:
   Ensures the sum of the binary variables correctly reflects the size constraints of the clique.
   $$\[
   H_A = A \left( 1 - \sum_{i=2}^N y_i \right)^2 + A \left( \sum_{i=2}^N i y_i - \sum_v x_v \right)^2
   \]$$
   where \( y_i \) are auxiliary binary variables representing the possible sizes of the clique, and \( x_v \) are binary variables indicating whether vertex \( v \) is included in the clique.

2. **Hamiltonian \( H_B \)**:
   Ensures the selected vertices form a complete subgraph.
   $$\[
   H_B = B \left[ \frac{1}{2} \left( \sum_{i=2}^N i y_i \right) \left( -1 + \sum_{i=2}^N i y_i \right) - \sum_{(u,v) \in E} x_u x_v \right]
   \]$$
   where \( (u,v) \in E \) represents the edges in the graph.

3. **Hamiltonian \( H_C \)**:
   Maximizes the number of vertices included in the clique.
   $$\[
   H_C = -C \sum_v x_v
   \]$$

### QUBO Formulation
The QUBO matrix \( Q \) is derived from the Hamiltonians, where the variables \( x_v \) and \( y_i \) are binary. The goal is to minimize the energy of the Hamiltonian to find the largest clique.


## Files

- `clique.ipynb`: This file contains the NP-Complete Version of the clique problem.
- `MAX_CLIQUE.ipynb`: This file contains the implementation of finding the largest clique in the graph which is NP-Hard.
- `MAX_CLIQUE.ipynb`: This file contains the implementation of finding the largest clique in the graph which is NP-Hard with log technique.

## Requirements

### Software
- Python 3.8+
- Required Python packages:
  - `dwave-ocean-sdk`
  - `networkx`
  - `matplotlib`
  - `numpy`
  - `scipy`

### Installation
1. Install Python 3.8+ from the [official website](https://www.python.org/downloads/).
2. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/largest-clique-quantum-annealing.git
   cd largest-clique-quantum-annealing
