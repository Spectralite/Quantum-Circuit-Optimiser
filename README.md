#  Quantum Circuit Optimiser

##  Overview

The **Quantum Circuit Optimiser** is a Python-based tool built with [Qiskit](https://qiskit.org/) to optimize quantum circuits for performance and compatibility with real quantum hardware. It leverages multiple optimization techniques — from commutative gate reordering to hardware-specific transpilation — to reduce circuit depth and gate count while preserving output fidelity.

This project includes implementations of **Grover’s** and **Shor’s** algorithms and demonstrates how ation strategies can significantly improve execution efficiency on NISQ-era devices.
---
##  Features

-  Supports Grover’s and Shor’s algorithm circuits  
-  Multi-level ation: basic, advanced, hardware-aware  
-  Graph-based circuit manipulation using Directed Acyclic Graphs (DAGs)  
-  Benchmarking: depth and gate count pre- and post-ation  
-  Simulation with `qasm_simulator` for validation  

---

##  Installation

Ensure Python 3.8+ is installed, then run:

```bash
pip install qiskit qiskit-aer
```
# Usage

## Running the Optimier

You can run the Optimiser from the command line interface with the following command:

```bash
python er.py --algorithm grover --optimization advanced --simulate
```
### Command Line Arguments

| Argument         | Description                                                  |
|------------------|--------------------------------------------------------------|
| `--algorithm`    | `grover` or `shor` |
| `--ation` | `basic`, `advanced`, or `hardware` optimization                     |
| `--simulate`     | Simulate both original and ed circuits                       |


### ation Strategies

####  Basic Simulations
The Basic simulations pass identifies and reorders commutable gate sequences to improve circuit depth. This approach targets simple patterns such as CZ commuting with X, allowing for effective reordering without affecting logical equivalence.

#### Advanced Simulations
The Advanced simulations pass leverages Qiskit's transpiler passes to further optimize the circuit:

- **RemoveResetInZeroState**: Eliminates unnecessary resets on qubits already in the |0⟩ state.
- **e1qGatesDecomposition**: Combines sequences of one-qubit gates into a more efficient single operation.
- **CommutativeCancellation**: Identifies and cancels pairs of gates that commute and nullify each other.

####  Hardware-Aware Simulation
The Hardware-Aware ation pass tailors the circuit to fit specific hardware constraints. It maps the circuit onto a predefined coupling map, reducing swap operations by strategically inserting BasicSwap operations. An example coupling map used is:

```python
CouplingMap([[0, 1], [1, 2], [2, 3], [3, 4]])
```
This ensures that operations are only applied to physically connected qubits, minimizing additional overhead and thus making the circuit more efficient.

### Simulation
The er allows you to simulate the circuit before and after optimization using Qiskit's `qasm_simulator`. This simulation helps verify that the optimized circuit maintains logical fidelity.

#### Example Output
```yaml
Original - Depth: 18, Gates: 35
ed - Depth: 10, Gates: 21

Original Simulation: {'00': 0.48, '11': 0.46, '01': 0.06}
ed Simulation: {'00': 0.49, '11': 0.45, '01': 0.06}
```
### Internal Architecture

The Quantum Circuit er uses **Directed Acyclic Graphs**  to represent quantum circuits. This conversion, done via Qiskit's **circuit_to_dag** function, facilitates efficient manipulation and reordering of gates.

The er's internal process involves:

1. DAG Conversion: Converting the quantum circuit into a DAG for structural analysis.

2. Gate-Level ation: Reordering and merging gates based on commutative properties.

3. Advanced ation: Applying Qiskit transpiler passes to remove redundancies and simplify operations.

4. Hardware-Specific ation: Adapting the circuit layout based on a coupling map to minimize additional SWAP operations.

5. Simulation: Verifying that ations preserve the original circuit's logical behavior.

### Included Algorithms
* **Grover's Algorithm** A 2-qubit implementation demonstrating the core elements of Grover's search algorithm. The circuit employs Hadamard gates, controlled-Z (CZ) operations, and oracle inversions to illustrate how circuit depth can be reduced through ation.

* **Shor's Algorithm** 
A simplified 3-qubit version of Shor's algorithm, which includes Hadamard gates, CNOTs, and phase shift gates. 

Benchmarking
---
The er reports the following metrics to evaluate its effectiveness:

Circuit Depth: The maximum number of gate layers (time steps) in the circuit.

Gate Count: The total number of quantum gate operations.

Output Distributions: Quasi-probability distributions from simulations to ensure logical consistency.

Example benchmarking output:
```yaml
Original - Depth: 18, Gates: 35
ed - Depth: 10, Gates: 21
```

<ins>References</ins>

* Nielsen, M.A., & Chuang, I.L., Quantum Computation and Quantum Information, Cambridge University Press, 2010.

* Qiskit Documentation – https://qiskit.org/documentation
