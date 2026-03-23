# ✅ Beginner Tasks for FPGA-SoC Learning (Zynq Platform)

These tasks align with the module-based learning path for Zynq FPGA-SoC platforms and are tailored for beginners to build skills progressively.

---

## 🔰 Module 1 – Introduction to FPGA-SoC Hybrid Systems

- [ ] Identify PS and PL components in Zynq using a Vivado block diagram.
- [ ] Create a basic Vivado project with Zynq Processing System and run Block Automation.
- [ ] Blink an LED using PS-controlled GPIO via a bare-metal C program.
- [ ] Explore Vivado and Vitis GUI: Identify the purpose of each tool.

---

## 🔰 Module 2 – Advanced FPGA Design Techniques

- [ ] Write a simple function (e.g., `int add(int a, int b)`) in C and synthesize with Vitis HLS.
- [ ] Export the HLS-generated IP and add it to a Vivado block design.
- [ ] Connect the custom IP to PS via AXI-Lite interface.
- [ ] Write a Vitis host application to configure and run the IP.
- [ ] Explore AXI signals and visualize read/write transactions in Vivado.

---

## 🔰 Module 3 – Linux on FPGA-SoC Systems

- [ ] Boot a PetaLinux image on your Zynq board via SD card or UART.
- [ ] Modify boot arguments in U-Boot and observe kernel changes.
- [ ] Locate GPIO or UART nodes in the Linux Device Tree.
- [ ] Use `/dev/mem` or UIO to access hardware IPs from user-space.
- [ ] Write a simple kernel module that prints "Hello FPGA" on insertion.

---

## 🔰 Module 4 – FPGA-Accelerated Computing

- [ ] Implement a basic vector addition accelerator in HLS.
- [ ] Measure and compare execution time between software and hardware versions.
- [ ] Integrate AXI DMA to accelerate large data transfers.
- [ ] Build a 3x3 image filter (e.g., blur or edge detection) and accelerate it.
- [ ] Use Vivado ILA to monitor signals between PS and PL during execution.

---

## 🔰 Module 5 – Performance Analysis and Optimization

- [ ] Profile software and hardware matrix multiplication using `gettimeofday()` or `perf`.
- [ ] Identify potential system bottlenecks (e.g., slow bus access, memory latency).
- [ ] Apply HLS optimization directives (`pipeline`, `unroll`, `inline`) and analyze their effect.
- [ ] Generate and interpret HLS/Vivado utilization and timing reports.

---

## 🔰 Module 6 – Real-time Systems and HW/SW Co-design

- [ ] Partition a real-time task (e.g., FIR filter) across PS and PL.
- [ ] Set a latency constraint in HLS and ensure timing is met.
- [ ] Perform co-simulation in Vitis HLS or Vivado using C testbenches.
- [ ] Use Vitis debugger (GDB) to step through code that communicates with FPGA logic.

---

## 🔰 Module 7 – Advanced Linux and System Integration

- [ ] Write a simple Linux character driver to interface with a memory-mapped IP.
- [ ] Use the UIO framework to expose FPGA registers to user-space applications.
- [ ] Compare data transfer speed between user-space (UIO) and kernel-space drivers.
- [ ] Optimize boot time by disabling unused services and modules.
- [ ] Monitor PL and PS utilization using tools like `top`, `htop`, and hardware counters.

---

## 🧠 Bonus Challenges (Applicable to Any Module)

- [ ] Create a custom "Hello World" IP in Verilog and connect it via AXI-Lite.
- [ ] Control your IP from a Linux user-space application via `/dev/uioX`.
- [ ] Join an FPGA-related forum (e.g., Xilinx, Digilent) and post a question or solution.
- [ ] Install and try a PYNQ overlay and control it using Python.
- [ ] Document your project (block diagram, IP settings, flow) in a markdown or PDF report.

---

**Tip**: Start with small wins (like toggling GPIO or reading registers) and build up to DMA, HLS, and kernel modules.

Happy hacking! 🔧📟🚀
