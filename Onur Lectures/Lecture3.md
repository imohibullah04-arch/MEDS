# Study Guide: Sequential Logic (Lecture 3)

## 1. The Power of Memory
Combinational logic is great but it has no memory. To build a computer that can follow a sequence of steps, we need *Sequential Logic*. This is the difference between a lock that opens when you set the right numbers (Combinational) and a dial lock that requires a specific sequence of turns (Sequential).



## 2. The Basic Storage Unit: The Latch
We start by tricking standard gates into remembering things.

### The Cross-Coupled Inverter
If you take two inverters and feed the output of one back into the input of the other, you create a circle that can hold a 1 or a 0 indefinitely. 
*   *The Problem:* There is no way to change the value once it is set. It is a memory you cannot write to.

### The RS Latch (Reset-Set)
By using NAND or NOR gates instead of inverters, we add control wires:
*   *Set (S):* Forces the output to 1.
*   *Reset (R):* Forces the output to 0.
*   *The "Forbidden" State:* You should never try to Set and Reset at the exact same time. It breaks the logic and can lead to *Metastability*, where the circuit gets stuck between 0 and 1 while oscillating wildly.



### The Gated D Latch
To make things safer, we add a "Write Enable" signal. The output only follows the data input (D) when the enable is high. This prevents accidental changes.

## 3. From Latches to Registers and Memory
Once we can store one bit, we can store anything.

*   *Register:* Simply a row of latches that share a single Write Enable signal. If you want to store a 4-bit number, you use four latches in parallel.
*   *Memory Array:* This is a grid of registers. We use a *Decoder*  to pick which specific address we want to talk to, and a *Multiplexer* to read the data out. 
    *   Note: Most of a modern CPU is actually just different types of memory such as caches and registers.



## 4. The Problem with Latches: Transparency
Latches are level-sensitive, meaning as long as the enable is high, the output changes as soon as the input does. This is dangerous for complex math because the data might change before the calculation is finished.

### The Solution: The D Flip-Flop
A Flip-Flop is edge-triggered. It only looks at the input for a split second when the clock signal jumps from 0 to 1. 
*   *How it is built:* It uses two latches in a Master-Slave configuration. The first one catches the data, and the second one releases it only on the clock's edge. This ensures the data is stable for the entire rest of the clock cycle.



## 5. Finite State Machines (FSM)
This is the brain of the circuit. An FSM moves through a series of *States*, like a traffic light moving from Green to Yellow to Red.
*   *Current State:* Stored in a register (Flip-Flops).
*   *Next State Logic:* Combinational logic that decides where to go next based on current state and inputs.
*   *Output Logic:* Decides what to do, such as turning on the Green light.



## 6. Synchronous vs. Asynchronous
*   *Synchronous:* Everything happens on the beat of a global *Clock*. This is how almost all modern computers work because it is much easier to design and debug.
*   *Asynchronous:* No clock; parts just talk to each other as fast as they can. While theoretically faster, it is incredibly difficult to prevent errors and race conditions.

### Pro-Tip for Students:
Think of the *Clock* as a heartbeat. It synchronizes billions of transistors so they all take a step at the same time. Without that heartbeat, the computer would quickly descend into logical chaos.
