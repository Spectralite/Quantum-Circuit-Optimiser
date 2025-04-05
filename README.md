# 🧠 Quantum Circuit Optimizer

## 🔬 Overview

The **Quantum Circuit Optimizer** is a Python-based tool built with [Qiskit](https://qiskit.org/) to optimize quantum circuits for performance and compatibility with real quantum hardware. It leverages multiple optimization techniques — from commutative gate reordering to hardware-specific transpilation — to reduce circuit depth and gate count while preserving output fidelity.

This project includes implementations of **Grover’s** and **Shor’s** algorithms and demonstrates how optimization strategies can significantly improve execution efficiency on NISQ-era devices.

---

## ✨ Features

- ✅ Supports Grover’s and Shor’s algorithm circuits  
- 🔁 Multi-level optimization: basic, advanced, hardware-aware  
- 🧱 Graph-based circuit manipulation using Directed Acyclic Graphs (DAGs)  
- 📊 Benchmarking: depth and gate count pre- and post-optimization  
- 🧪 Simulation with `qasm_simulator` for validation  

---

## 📦 Installation

Ensure Python 3.8+ is installed, then run:

```bash
pip install qiskit qiskit-aer

Usage
Running the Optimizer
You can run the quantum circuit optimizer from the command line interface (CLI) with the following command:

bash
Copy
Edit
python optimizer.py --algorithm grover --optimization advanced --simulate
Command Line Arguments
Argument	Description
--algorithm	Choose grover or shor algorithm
--optimization	Choose basic, advanced, or hardware optimization
--simulate	Simulate both original and optimized circuits
