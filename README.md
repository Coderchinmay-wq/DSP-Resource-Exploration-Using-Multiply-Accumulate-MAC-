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
