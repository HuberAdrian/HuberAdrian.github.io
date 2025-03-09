---
layout: project
title: "Quantum Circuit Simulator"
date: 2022-03-15
featured_image: /wp-content/uploads/2022/03/quantum-simulator.jpg
github_url: https://github.com/username/quantum-simulator
demo_url: https://quantum-demo.adrian-huber.org
technologies:
  - JavaScript
  - React
  - MathJS
  - D3.js
usemathjax: true
---

## Project Overview

The Quantum Circuit Simulator is a browser-based educational tool that allows users to build quantum circuits and visualize quantum states in real-time. This project aims to make quantum computing concepts more accessible to students and enthusiasts by providing an intuitive interface for experimentation.

<div style="text-align:center">
<img src="/wp-content/uploads/2022/03/quantum-simulator-interface.png" alt="Quantum Simulator Interface" style="width: 70%; height: auto;">
</div>

## Key Features

### Interactive Circuit Builder

Users can drag and drop quantum gates onto a circuit canvas, connecting multiple qubits and creating complex quantum algorithms. The interface supports:

- Standard gates: Hadamard, X, Y, Z, S, T
- Multi-qubit gates: CNOT, SWAP, Toffoli
- Measurement operations
- Custom gate definitions

### Real-time State Visualization

As users build circuits, the simulator calculates and displays:

- State vector representation
- Probability amplitudes
- Bloch sphere visualization for single-qubit states
- Quantum circuit matrix representation

### Educational Components

The simulator includes several educational features:

- Step-by-step execution to understand how quantum states evolve
- Detailed explanations of each gate's mathematical properties
- Built-in tutorials for common quantum algorithms
- Export functionality for sharing circuits

## Technical Implementation

The simulator was built using modern web technologies to ensure accessibility without requiring any installation:

- Frontend framework: React with TypeScript
- State vector calculations: Custom linear algebra library optimized for sparse matrices
- Visualizations: D3.js for interactive diagrams
- Mathematical typesetting: MathJax for displaying equations

The core simulation engine implements the mathematical formalism of quantum computing:

$$
|\psi\rangle = \sum_{i=0}^{2^n-1} \alpha_i |i\rangle
$$

Where $|\psi\rangle$ represents the quantum state, $n$ is the number of qubits, and $\alpha_i$ are complex probability amplitudes.

## Future Directions

Future development plans include:

1. Adding support for quantum error correction codes
2. Implementing noise models to simulate real quantum hardware
3. Creating a library of advanced quantum algorithms
4. Adding a collaborative feature for multiple users to work on the same circuit

## User Feedback

The simulator has been used in undergraduate quantum computing courses at several universities, with positive feedback on its intuitive interface and educational value.

> "This simulator helped me understand quantum superposition in a way textbooks never could." - Computer Science Student