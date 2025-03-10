---
layout: project
title: "Quantum Factorization with Shor's Algorithm"
date: 2025-02-03
featured_image: /wp-content/uploads/2025/03/quantum-factorization.png
github_url: https://github.com/HuberAdrian/MIT_iQuHack_2025
technologies:
  - Quantum Computing
  - Python
  - Quantum Rings SDK
  - Shor's Algorithm
usemathjax: true
---

# Quantum Factorization Challenge - MIT iQuHack 2025

MIT iQuHACK (interdisciplinary Quantum HACKathon) is MIT's annual quantum computing competition. The 2025 edition ran from January 31 to February 2, featuring both in-person work on real quantum hardware and virtual challenges on simulators. I participated virtually in the Quantum Rings challenge.

## Project Overview

For the Quantum Rings challenge at iQuHack, I implemented Shor's algorithm to factor semiprime numbers. Using the Quantum Rings Simulator with 200+ available qubits, I built a quantum circuit that factored 12-bit semiprimes like 3127 and 3131. 

## The Problem: Period Finding with Quantum Phase Estimation

A semiprime number N is the product of exactly two prime numbers p and q. While multiplication is computationally trivial, factorization becomes exponentially harder as the number grows larger. This property forms the foundation of cryptographic systems like RSA.

$$N = p \times q \text{ where } p \text{ and } q \text{ are prime numbers}$$

Shor's algorithm solves this by reducing factorization to period-finding:

1. For a semiprime N and a randomly chosen coprime number a
2. Find the period r where: $a^r \mod N = 1$
3. Use r to find factors of N with high probability

### The Quantum Part: Phase Estimation

The core quantum component uses quantum phase estimation on the unitary operator:

$$U\vert y\rangle \equiv \vert ay \mod N\rangle$$

Key steps:
1. Initialize superposition in counting register using Hadamard gates
2. Apply controlled modular multiplications
3. Use inverse quantum Fourier transform
4. Measure to obtain phase s/r
5. Use classical post-processing (continued fractions) to find r

## Implementation for 12-bit Numbers

The implementation I did handles 12-bit semiprime numbers (like 3127 = 53 × 59). This requires:
- 12 qubits for counting register (phase estimation)
- 13 qubits for work register (modular arithmetic, ceil(log₂(N)) + 1)
- Total circuit depth of about 781 gates

### Key Code Components

My implementation uses the native Quantum Rings SDK to build and run the circuit. Although you can also run qiskit based circuits, I wanted to try the native approach from Quantum Rings. Here's a look at the main components:

```python
def factor_semiprime(N, backend):
    """Main function implementing Shor's algorithm for 12-bit numbers."""
    # Find coprime a
    a = 2
    while math.gcd(a, N) != 1:
        a += 1
    
    # Circuit parameters
    n_count = 12  # 12 counting qubits for 12-bit numbers
    target_size = math.ceil(math.log(N, 2)) + 1
    
    # Create quantum circuit
    qr = QuantumRegister(n_count + target_size, 'q')
    cr = ClassicalRegister(n_count, 'c')
    qc = QuantumCircuit(qr, cr)
    
    # Initialize counting register with Hadamard gates
    for q in range(n_count):
        qc.h(qr[q])
    
    # Initialize target register
    qc.x(qr[n_count])
    
    # Controlled modular exponentiation
    for q in range(n_count):
        power = 2**q
        c = pow(a, power, N)
        for i in range(target_size):
            if (c >> i) & 1:
                qc.cx(qr[q], qr[n_count + i])
    
    # Inverse QFT
    for j in range(n_count):
        for m in range(j):
            angle = -math.pi / float(2**(j-m))
            qc.cu1(angle, qr[m], qr[j])
        qc.h(qr[j])
```

For full implementation including the classical post-processing, check the [GitHub repository](https://github.com/HuberAdrian/MIT_iQuHack_2025/blob/main/12bit_semiprimes.ipynb).

## Results

Running the algorithm on the Quantum Rings simulator with 2048 shots yielded successful factorizations:

```
Factoring N = 3127 (bit size 12)
Job Queued
Job Running
Job Running
Job Done.
Ending Job Monitor
Successfully factored 3127 = 59 * 53

Factoring N = 3131 (bit size 12)
Job Queued
Job Running
Job Running
Job Done.
Ending Job Monitor
Successfully factored 3131 = 31 * 101
```

The algorithm consistently found the correct factors after processing the quantum phase estimation results through the classical post-processing steps.

## Scalability Analysis

While successful for 12-bit numbers, the implementation faces scaling challenges:

- Qubit requirements increase with number size (roughly 2n counting qubits for n-bit numbers)
- Circuit depth grows at O(n³), making larger factorizations computationally intensive
- The current implementation uses 12 counting qubits and 13 work qubits (25 total)

To tackle larger semiprimes (which would be more relevant for cryptography), several optimizations would be needed:

- More efficient modular multiplication circuits
- Improved phase estimation techniques
- Potential tradeoffs between precision and qubit count

The transition from 12-bit to larger numbers isn't just a matter of adding more qubits - the circuit complexity and error rates become significant barriers that require algorithmic improvements.

## Conclusion

This implementation of Shor's algorithm demonstrates quantum computing's potential to tackle problems that are challenging for classical computers. The successful factorization of 12-bit semiprimes (3127 and 3131) confirms the algorithm works as expected, though simulator constraints limited our explorations to relatively small numbers.

With access to more qubits, this approach could scale to larger numbers with optimization, highlighting the potential paradigm shift quantum computing represents for cryptography.

## Participation Certificate

<div style="text-align:center">
<a href="/wp-content/uploads/2025/03/iquhack-certificate.pdf">
<img src="/wp-content/uploads/2025/03/iquhack-certificate-thumbnail.png" alt="MIT iQuHack 2025 Participation Certificate" style="width: 70%; height: auto;">
</a>
</div>

I received a participation certificate for MIT iQuHack 2025. You can verify my participation using the hash: 8bfd6f1d at the [official iQuHack verification page](https://www.iquise.mit.edu/iQuHACK/2025-01-31).