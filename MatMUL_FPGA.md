# 🧪 Lab Guide: FPGA Acceleration of Matrix Multiplication on Zynq Using Vitis

---

## ✅ 1. Lab Objectives

- Implement **matrix multiplication** using C/C++ and accelerate it with **Vitis HLS**.
- Convert the function to a **hardware IP core** for the FPGA.
- Integrate the IP into a **Vivado block design** connected to the Zynq PS.
- Run matrix multiplication from ARM processor (PS) and compare:
  - Software-only execution (CPU)
  - Hardware-accelerated execution (FPGA)

---

## 🛠 2. Prerequisites

- **Hardware**: Zynq board (ZedBoard, Zybo, Ultra96, etc.)
- **Software**:
  - Vivado Design Suite
  - Vitis + Vitis HLS
  - (Optional) PetaLinux
- Knowledge of:
  - C/C++ programming
  - AXI protocol basics
  - Zynq SoC architecture

---

## 📁 3. Project Structure
```
fpga_matrix_mul_lab/
├── hls_matrix_mul/ # Vitis HLS project for matrix multiplication
├── vivado_design/ # Vivado block design & bitstream
├── host_app/ # C app to run on Zynq ARM
└── petalinux_project/ # Optional Linux project with device tree
```

---

## 🚀 4. Step-by-Step Instructions

### 🔧 4.1 Implement Matrix Multiplication in Vitis HLS

#### a. Launch Vitis HLS

```bash
vitis_hls
```
b. Create a New Project
Name: hls_matrix_mul

Top Function: matrix_mul

Language: C++

Target: Your Zynq device (e.g., xc7z020clg400-1)

c. Function Code: matrix_mul.cpp
```cpp
#define SIZE 4

void matrix_mul(int A[SIZE][SIZE], int B[SIZE][SIZE], int C[SIZE][SIZE]) {
#pragma HLS INTERFACE s_axilite port=return bundle=CTRL
#pragma HLS INTERFACE s_axilite port=A bundle=CTRL
#pragma HLS INTERFACE s_axilite port=B bundle=CTRL
#pragma HLS INTERFACE s_axilite port=C bundle=CTRL

    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
#pragma HLS PIPELINE
            C[i][j] = 0;
            for (int k = 0; k < SIZE; k++) {
                C[i][j] += A[i][k] * B[k][j];
            }
        }
    }
}
```
###  d. Synthesize and Export IP
-   From Vitis HLS: Run C Synthesis
-   Export RTL as Vivado IP Package

## 🧱 4.2 Vivado Block Design Integration
### a. Create a Vivado Project
-   Add Zynq Processing System
-   Run Block Automation
-   Add the matrix_mul IP from the IP Catalog
-   Connect via AXI-Lite to Zynq GP Master
-   Auto-connect clocks and resets
### b. Generate Bitstream & Export Hardware
-   Validate the design
-   Generate bitstream
-   File → Export → Export Hardware (with bitstream)
-   Save the .xsa file for use in Vitis

## 🖥 4.3 Host Application in Vitis
### a. Create Platform & Application Projects
-   Import .xsa into a Vitis workspace
-   Create a new Application project named host_app
-   Target: ps7_cortexa9_0
####    Language: C
###     b. Sample Host Code: main.c
```c
#include "xmatrix_mul.h"
#include "xparameters.h"
#include <stdio.h>

#define SIZE 4

int main() {
    XMatrix_mul matmul;
    int A[SIZE][SIZE] = {
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9, 1, 2, 3},
        {4, 5, 6, 7}
    };
    int B[SIZE][SIZE] = {
        {1, 0, 0, 0},
        {0, 1, 0, 0},
        {0, 0, 1, 0},
        {0, 0, 0, 1}
    };
    int C[SIZE][SIZE];

    XMatrix_mul_Initialize(&matmul, XPAR_MATRIX_MUL_0_DEVICE_ID);
    XMatrix_mul_Set_A(&matmul, (u32)A);
    XMatrix_mul_Set_B(&matmul, (u32)B);
    XMatrix_mul_Set_C(&matmul, (u32)C);
    XMatrix_mul_Start(&matmul);

    while (!XMatrix_mul_IsDone(&matmul));

    printf("Result:\n");
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf("%d ", C[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```
##  🐧 4.4 Run on Zynq Board
-   Load the bitstream (via Vitis or U-Boot)
-   Boot Linux
-   Transfer the ELF file to the board
-   Run the program and check the results

##  📊 5. Performance Comparison
### Software-Only Version (For Comparison)
```c
void sw_matrix_mul(int A[SIZE][SIZE], int B[SIZE][SIZE], int C[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++)
        for (int j = 0; j < SIZE; j++) {
            C[i][j] = 0;
            for (int k = 0; k < SIZE; k++) {
                C[i][j] += A[i][k] * B[k][j];
            }
        }
}
```
##  Measure Time
-   Use gettimeofday() or clock() to compare CPU vs FPGA execution times:

```c
#include <sys/time.h>
struct timeval start, end;
gettimeofday(&start, NULL);
// Run function
gettimeofday(&end, NULL);
long time = (end.tv_sec - start.tv_sec) * 1000000 + (end.tv_usec - start.tv_usec);
printf("Execution time: %ld us\n", time);
```
##  📌 6. Summary
####    By completing this lab, you:
-   Designed a hardware IP for matrix multiplication using Vitis HLS.
-   Integrated the IP into the Zynq SoC using Vivado.
-   Wrote a host application to control the accelerator via AXI.
-   Demonstrated performance improvement using FPGA acceleration.

##  🧩 Optional Extensions
-   Increase matrix size (e.g., 8×8 or 16×16)
-   Add AXI DMA for faster memory transfer
-   Use AXI-Stream interfaces instead of AXI-Lite
-   Apply HLS optimizations: UNROLL, ARRAY_PARTITION, PIPELINE, etc.
```yaml

---

Let me know if you want this as a downloadable `.md` file or ZIP archive with templates. I can generate those next.
```