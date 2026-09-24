# DSP Resource Exploration Using MAC Unit

## 📌 Overview

This experiment demonstrates the implementation of a **Multiply-Accumulate (MAC)** operation using **Vitis HLS** and analyzes the FPGA resources utilized by the generated hardware.

The implemented operation is:

\[
Output = (A \times B) + C
\]

The experiment focuses on understanding how arithmetic operations, particularly multiplication, are mapped onto dedicated **DSP slices** in an FPGA.

---

## 🎯 Objectives

- Understand FPGA DSP slices.
- Implement a MAC operation using Vitis HLS.
- Perform C simulation to verify functional correctness.
- Perform C synthesis to generate RTL hardware.
- Analyze FPGA resource utilization.
- Study the relationship between multiplication and DSP utilization.
- Understand the RTL/hardware representation generated from C/C++ code.

---

## 🛠️ Tools Used

- **AMD Vitis Unified IDE 2026.1**
- **Vitis HLS**
- Target FPGA: **Artix-7**
- Device: `xc7a100tcsg324-1`
- HLS Clock Target: **10 ns (100 MHz)**

---

## 💻 Design

### MAC Function

```cpp
int mac(int A, int B, int C)
{
    return (A * B) + C;
}
```

## Testbench

The design was verified using the following test cases:

| Test |  A |  B |  C | Expected Output |
| ---- | -- | -- | -- | --------------- |
| 1    | 10 |  5 |  3 |              53 |
| 2    |  8 |  7 |  4 |              60 |
| 3    | 12 |  6 |  9 |              81 |

## 🧪 C Simulation

The C simulation was completed successfully with 0 errors.

### Simulation Output
```
Test 1: 53
Test 2: 60
Test 3: 81
```
The simulation confirms that the MAC function produces the expected results.

## ⚙️ C Synthesis

C synthesis was successfully completed in Vitis HLS.

The C/C++ implementation was converted into RTL hardware targeting the `xc7a100tcsg324-1` Artix-7 device.
| Parameter       |     Result |
| --------------- | ---------: |
| Target Clock    |   10.00 ns |
| Estimated Clock |   6.860 ns |
| Estimated Fmax  | 145.77 MHz |

## 📊 Resource Utilization

The synthesis report produced the following resource estimates:
| FPGA Resource | Utilization |
| ------------- | ----------: |
| LUT           |         106 |
| FF            |         200 |
| BRAM          |           0 |
| DSP           |           3 |

## 🔍 Hardware Interfaces

The synthesized design contains the following interfaces:
| Port        | Direction |  Width |
| ----------- | --------- | -----: |
| A           | Input     | 32-bit |
| B           | Input     | 32-bit |
| C           | Input     | 32-bit |
| `ap_return` | Output    | 32-bit |

The generated HLS control interface includes:

- `ap_clk`
- `ap_rst`
- `ap_ctrl_hs`

## 🔧 Bind Operation Analysis

The synthesis report shows that the multiplication operation:

`A × B`

is mapped to DSP resources.

The addition operation:

`(A × B) + C`

is implemented as part of the generated hardware datapath.

## 📈 Performance

The synthesized MAC module has an estimated latency of approximately 20 ns with an initiation interval of 3 cycles according to the Vitis HLS synthesis report.

The target clock period was 10 ns, while the estimated achievable clock period was 6.860 ns.

## 🧠 Key Learning
### Why are DSP slices used?

FPGA DSP slices are dedicated hardware resources optimized for arithmetic operations such as:

Multiplication
Addition
Multiply-Accumulate
Signal-processing operations

Using DSP resources can provide better arithmetic performance and reduce the amount of general-purpose FPGA logic required for multiplication.

### Why is BRAM utilization zero?

The MAC design does not contain arrays, buffers, or large memory structures. Therefore, no Block RAM is required.

## 🔬 Design Comparison
### Design A
`Output = A + B`

This design does not require multiplication and therefore does not inherently require DSP resources.

Design B
`Output = (A × B) + C`

This design contains multiplication and therefore uses DSP resources.

### Extended Design

If the design is changed to:

`Output = A × B + C × D`

there are two multiplication operations. DSP utilization is therefore expected to increase, depending on synthesis optimization and resource sharing.

## 📸 Screenshots
C Simulation

Synthesis Report

Hardware Interfaces

Bind Operation Report

## 📚 Experiment Outcome

After completing this experiment, the following concepts were understood:

1. FPGA DSP slices.
2. MAC implementation using Vitis HLS.
3. C simulation and verification.
4. C synthesis and RTL generation.
5. FPGA resource utilization.
6. DSP mapping of multiplication operations.
7. HLS-generated hardware interfaces.
8. Timing and latency analysis.

## 📁 Project Structure
```
DSP-Resource-Exploration/
│
├── README.md
│
├── src/
│   ├── mac.cpp
│   └── mac_tb.cpp
│
├── screenshots/
│   ├── c-simulation.png
│   ├── synthesis-report.png
│   ├── hardware-interfaces.png
│   └── bind-op-report.png
│
└── report/
    └── DSP_Resource_Exploration_Completed.docx
```
## 👨‍💻 Author

Chinmay Yalawatti

Electronics & Communication Engineering
KLE Technological University
