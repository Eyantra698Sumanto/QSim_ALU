# Quantum Computing Hackathon July 2023 by CDAC
# QSim_ALU
This repository contains Qiskit code to simulate an ALU using QSim
## Table of Contents
- [Steps to run the code](#steps-to-run-the-code)
- [Code Description](#code-description)
  * [Import packages](#import-packages)
  * [Create quantum and classical registers](#create-quantum-and-classical-registers)
  * [Create quantum circuit](#create-quantum-circuit)
  * [Set inputs](#set-inputs)
  * [Convert inputs to binary strings](#convert-inputs-to-binary-strings)
  * [Set input bits](#set-input-bits)
  * [Perform ALU operations](#perform-alu-operations)
  * [Measure the output bits](#measure-the-output-bits)
  * [Execute the circuit on the density matrix simulator](#execute-the-circuit-on-the-density-matrix-simulator)
  * [Print the density matrix of the final state](#print-the-density-matrix-of-the-final-state)
- [Output](#output)
  * [Quantum circuit for addition](#quantum-circuit-for-addition)
  * [QSim Output](#qsim-output)
- [Contributer](#contributer)

## Steps to run the code
### Using QSim
1. Register on the QSim Portalhttps://qctoolkit.in)
2. Log in to QSim along with your given Username and Password.
3. Paste the **[Code](https://github.com/Eyantra698Sumanto/QSim_ALU/blob/main/code/ALU.py)** in the QSim editor.</br>
 ![image](https://github.com/Eyantra698Sumanto/QSim_ALU/assets/58599984/1f2eb3c9-07b8-4bf6-b5fa-ea5eca3cc996)
5. Click on the run circuit button:
![image](https://github.com/Eyantra698Sumanto/QSim_ALU/assets/58599984/9e5f7ab5-6ab7-43ca-af68-1763f2d6a12b)
### Using Blender
1. Run Blender by clicking on the following **[LINK](https://mybinder.org/v2/gh/indian-institute-of-science-qc/qiskit-aakash/bea98fbff86c234c0b1990add17493a1e86917cb?labpath=dm_simulator_user_guide)**.
2. Open a New Notebook.
3. Upload the .ipynb file at following **[LINK](https://github.com/Eyantra698Sumanto/QSim_ALU/blob/main/code/alu.ipynb)**.
4. Click on **Restart Kernal and All Cells** button.
5. Now all the cells will be run!
## Code Description
### Import packages
```
from qiskit import QuantumRegister, ClassicalRegister
from qiskit import QuantumCircuit, execute, BasicAer
import numpy as np
```
### Create quantum and classical registers
```
q = QuantumRegister(10, 'q')
c = ClassicalRegister(10, 'c')  # Output registers
```
### Create a quantum circuit
```
qc = QuantumCircuit(q, c)
```
### Set inputs
```
input_1 = 5
input_2 = 3
operation = 'Multiplication'
```
### Convert inputs to binary strings
This step is needed since the inputs will be in the binary string format.
```
bin_input_1 = format(input_1, '03b')
bin_input_2 = format(input_2, '03b')
```
### Set input bits
```
for i, bit in enumerate(bin_input_1):
    if bit == '1':
        qc.x(q[i + 2])  # Apply X gate to q[2] and q[3]
for i, bit in enumerate(bin_input_2):
    if bit == '1':
        qc.x(q[i + 4])  # Apply X gate to q[4] and q[5]
```
### Perform ALU operations
1. Addition
2. Substraction
3. Multiplication
4. Division
5. XOR
6. AND
7. OR
8. NOT</br>
**Example of Addition:**
```
  qc.cx(q[3], q[0])  # Swap q[3] and q[0]
  qc.cx(q[4], q[0])  # XOR
  qc.ccx(q[3], q[4], q[0])  # AND
```
### Measure the output bits
```
qc.measure(q[0], c[0])
qc.measure(q[1], c[1])
qc.measure(q[4], c[2])
qc.measure(q[2], c[3])
```
### Execute the circuit on the density matrix simulator
```
backend = BasicAer.get_backend('dm_simulator')
job = execute(qc, backend=backend, **options)
job_result = job.result()
```

### Print the density matrix of the final state
```
density_matrix = job_result.results[0].data.densitymatrix
print(density_matrix)
```
## Output
### Quantum circuit for addition
![image](https://github.com/Eyantra698Sumanto/QSim_ALU/assets/58599984/f251f7ef-a8a2-4264-9f39-a5c70b93ad86)
### QSim Output 
![image](https://github.com/Eyantra698Sumanto/QSim_ALU/assets/58599984/b276fc1e-521c-41d9-83fb-c8eb020ce920)
## Acknowlgements
1. CDAC Team
2. IIT Roorkee
3. IISc Bangalore
4. All other organizers
## Contributer
Sumanto Kar</br>
Student and Project Staff, IIT Bombay
Contact: jeetsumanto123@gmail.com
## Thank You!
