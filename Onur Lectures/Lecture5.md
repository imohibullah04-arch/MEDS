# Study Guide: SystemVerilog for Sequential Logic (Lecture 5)

## 1. The Shift to Sequential Coding
In the previous lecture, we focused on combinational logic where outputs change instantly. Now, we use SystemVerilog to describe circuits that have a memory of past events. This requires us to use "procedural blocks" instead of just simple assign statements.

## 2. Always Blocks
The always block is the core of sequential design. It tells the hardware to wait for a specific event before updating.
*   *always_comb:* Used for combinational logic. It ensures the tool knows you are trying to build gates, not memory.
*   *always_ff:* Specifically used to describe Flip-Flops. It requires a "sensitivity list" to tell it exactly when to trigger.

## 3. Describing the D Flip-Flop
To build a Flip-Flop in code, we use the @ symbol to listen for the clock edge.
*   *The Code:* always_ff @(posedge clk) tells the circuit to only update the output at the exact moment the clock signal rises from 0 to 1.
*   *Resets:* Most Flip-Flops need a reset signal to start at a known state. You can describe an "asynchronous reset" by adding it to the sensitivity list: always_ff @(posedge clk or posedge reset).

## 4. Blocking vs. Non-Blocking Assignments
This is the most critical distinction in HDL programming:
*   *Blocking (=):* Used in always_comb. These happen one after another, just like software.
*   *Non-Blocking (<=):* Used in always_ff. These happen "in parallel" at the clock edge. This prevents "race conditions" where one flip-flop might accidentally see the new value of another before it is ready.

## 5. Coding Finite State Machines (FSM)
To design a brain for your circuit, you usually follow a three-block coding style:
1.  *State Register:* An always_ff block that simply updates the "current state" to the "next state" on the clock edge.
2.  *Next State Logic:* An always_comb block (usually using a case statement) that decides what the next state should be based on current inputs.
3.  *Output Logic:* An always_comb block that decides what the circuit should do in each state.

## 6. The Power of Case Statements
Using case or if-else inside procedural blocks makes the code much more readable than writing out massive Boolean equations. You can simply list your states (e.g., IDLE, S1, S2) and describe the transitions logically.

### Pro-Tip:
Never mix Blocking and Non-Blocking assignments in the same block. A simple rule of thumb: use <= for anything triggered by a clock and = for everything else. This keeps your hardware predictable and prevents strange bugs during simulation.