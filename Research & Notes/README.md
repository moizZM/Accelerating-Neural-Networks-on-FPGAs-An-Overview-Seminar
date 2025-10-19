# Notes

## Main topic: Accelerating Neural Networks on FPGAs

Sub-questions:

> 1: What is FPGA architecture and why is it suitable for neural networks?

> 2:What are the design frameworks (e.g., Xilinx Vitis AI, Intel OpenVINO)?

> 3: What are the common FPGA acceleration techniques (parallelism, pipelining, quantization)?

> 4: How do FPGAs compare to CPUs/GPUs for NN workloads?

> 5: What challenges exist (memory bandwidth, resource utilization, development time)?

> 6: What are future research directions (dynamic reconfiguration, hybrid systems, etc.)?

### part 1: What is FPGA architecture and why is it suitable for neural networks?

**What is FPGA, How is it different from a microcontrooler?**
An FPGA is hardware that can be configured to do one specific job by connecting built in logic gates using VHDL or Verilog. You design the circuit itself  for example, a half adder, full adder, or 8 bit adder.
A microcontroller, on the other hand, has a fixed CPU that can run many different tasks through software, like reading sensors, lighting LEDs, or sending signals.

**what are neural networks**
A neural network is a computer model inspired by the human brain.
It’s made up of layers of neurons (nodes) that process information by performing many simple mathematical operations.
> **In short:**
> **A neural network is a system of interconnected nodes that learns from data to make predictions or decisions — similar to how the human brain processes information.**

**what is FPGA architecture?**
It is the internal structure of the FPGA like how it is built inside and lets us connect any digital circuite we want through VHD and other tools.
it contains 
1: logic blocks, look up tables , and flipflops to perform logic operations like (and , or , xor , xnor and etc)
2: I/O blocks : to intract with the fpga externally 
3: DSP bloks : speciallized unites fro fast math.
4: BlockRAM for storing memmory (on chip).

**why is it suitable for neural networks**
An FPGA is suitable for neural networks because it can be customized at the hardware level to match how neural networks work
1: Parallelism: Each neuron or layer can be built as its own hardware block, so thousands of operations happen at once.
2: Custom data paths: You can design the exact circuit for your model (e.g., convolution, activation), removing unnecessary steps.
3: Low latency & power: No software overhead data flows directly through hardware, making it fast and energy efficient.
4: Flexibility: You can reprogram it anytime for different models or optimizations.

### Part 2: What are the design frameworks (e.g., Xilinx Vitis AI, Intel OpenVINO)?
Design frameworks for FPGAs are software tools and platforms that help you develop, optimize, and deploy neural networks or other applications on FPGA hardware without manually designing every gate.

### Part 3: What are the common FPGA acceleration techniques (parallelism, pipelining, quantization)?
The common FPGA acceleration techniques are methods used to make neural networks run faster and more efficiently on FPGAs.

FPGAs accelerate neural networks by using parallelism, pipelining, quantization, and efficient memory handling  all **to achieve high speed, low latency, and low power.**

> 1. Parallelism
FPGAs can execute many operations at the same time.
You can create multiple processing units (e.g., neurons or MAC units) that work simultaneously.
Great for matrix multiplications and convolutions, which are common in neural networks.

> 2. Pipelining
Pipelining means breaking a big task into small steps that can work one after another, like an assembly line
Imagine a car factory  one worker installs the engine, the next paints it, and the next checks quality.
While worker 2 paints car #1, worker 1 is already putting the engine in car #2.
So many cars are being worked on at the same time, just at different stages.

It’s the same in an FPGA 
a big calculation is split into stages, and after the first few cycles, the circuit produces one new result every clock tick.

> 3. Quantization
Quantization means using smaller numbers to do calculations instead of big ones.

Normally, neural networks use 32-bit floating-point numbers (very detailed but heavy).
If we use 8-bit or 4-bit integers instead, the numbers are less detailed but still good enough for most tasks.
This makes the network:
* Use less memory
* Run faster
* Consume less power
FPGAs are great for this because you can design the hardware to work with any number size you want — 4-bit, 8-bit, or even 3-bit — something normal processors can’t easily do.

4. Data Reuse and Local Memory
   Data reuse and local memory means keeping important data close to the FPGA chip instead of fetching it again and again from external memory, which is slower.

In neural networks, things like weights and activations are used many times.
So instead of reading them from outside memory each time, the FPGA stores them temporarily in its on-chip Block RAM (BRAM)  a small, fast memory built inside the FPGA.

````
In a neural network, weights are the numbers that control how strongly one neuron affects another.

Here’s the simple idea 
Each connection between two neurons has a weight — like an importance level.
When data passes through the network, each input value is multiplied by its weight.
The network learns by adjusting these weights during training so that its predictions become more accurate.

Example:
If a neuron is checking whether an image has a cat:
The “whisker” feature might get a high weight (important).
The “background color” feature might get a low weight (less important).
So, weights = learned numbers that decide how much influence each input has on the final output.

```` 
### Part  4: How do FPGAs compare to CPUs/GPUs for NN workloads?

| Feature          | **CPU**                                      | **GPU**                                                             | **FPGA**                                                       |
| ---------------- | -------------------------------------------- | ------------------------------------------------------------------- | -------------------------------------------------------------- |
| **How it works** | Runs instructions one by one (sequentially). | Runs many instructions in parallel (using hundreds of small cores). | You build custom hardware that runs tasks fully in parallel.   |
| **Flexibility**  | Very flexible — can run any program.         | Also flexible but optimized for large math tasks.                   | Fully customizable hardware — you design exactly what it does. |
| **Speed**        | Slower for large neural networks.            | Very fast for training and large-scale inference.                   | Fast for *specific* models (especially inference).             |
| **Power use**    | High                                         | High                                                                | Much lower (very energy efficient).                            |
| **Best for**     | General computing, control tasks.            | Training and large-scale inference.                                 | Real-time, low-latency, edge or embedded AI.                   |


> CPUs are flexible but **slow for big neural networks**.
> GPUs are fast but **power hungry** .
> FPGAs are customizable you can design hardware that matches your neural network exactly, **giving high speed with low power for inference tasks**.


### Part  5: What challenges exist (memory bandwidth, resource utilization, development time)?

1. Memory Bandwidth
Neural networks need to move a lot of data (like weights and activations).
FPGAs have limited access speed to external memory (like DRAM).
If data moves too slowly, the whole system becomes bottlenecked, reducing performance.

2. Resource Utilization
FPGAs have a limited number of logic blocks, DSPs, and BRAM.
Large or complex neural networks might not fit completely on one FPGA.
Designers must carefully balance speed, precision, and hardware resources.

3. Development Time
Designing and testing FPGA hardware (VHDL, Verilog, or HLS) takes much longer than writing code for a CPU or GPU.
Toolchains like Vivado or Quartus are complex and require hardware knowledge.
Debugging and synthesis can take hours, slowing down development.

> In short:
### FPGAs are powerful but challenging because of limited memory speed, restricted hardware resources, and longer, more complex design processes.

### Part 6: What are future research directions (dynamic reconfiguration, hybrid systems, etc.)?
... 































































