# Lecture Summary: Timing & Verification II (L6)

## 1. Timing in Combinational Circuits
Real-world circuits do not change state instantaneously. Delay is primarily caused by *capacitance* and *resistance (RC delay)* within the transistors and wires.

### Key Timing Definitions:
*   *Propagation Delay :* The maximum time from an input change to the output finishing its change (the "worst-case" or longest path).
*   *Contamination Delay :* The minimum time from an input change to the output starting to change (the "best-case" or shortest path).

### Glitches
*   A *glitch* occurs when a single input transition causes multiple output transitions before settling.
*   *Cause:* Different paths through the logic have different delays (slow vs. fast paths).
*   *Significance:* Glitches consume unnecessary power but usually don't affect correctness if the system waits for the steady-state output.

---

## 2. Sequential Circuit Timing
For sequential elements like *D Flip-Flops, data must be stable during a specific window around the clock edge to avoid **metastability*.

### Flip-Flop Constraints:
*   *Setup Time ($t_{setup}$):* Time before the clock edge that data must be stable.
*   *Hold Time ($t_{hold}$):* Time after the clock edge that data must be stable.
*   *Aperture Time:* The total window ($t_{setup} + t_{hold}$) where data must not change.

### Propagation & Contamination:
*   *Clock-to-Q Propagation Delay ($t_{pcq}$):* Time after the clock edge for the output $Q$ to become stable.
*   *Clock-to-Q Contamination Delay ($t_{ccq}$):* Time after the clock edge for the output $Q$ to start changing.

---

## 3. Timing Constraints & Violations
In a system with two registers ($R1$ and $R2$) and combinational logic in between:

### Setup Time Constraint (Max Delay)
*   *Equation:* $T_c \geq t_{pcq} + t_{pd} + t_{setup}$
*   *Violation:* Occurs if the combinational logic is too slow.
*   *Fix:* Increase the clock period ($T_c$) or simplify the logic.

### Hold Time Constraint (Min Delay)
*   *Equation:* $t_{ccq} + t_{cd} \geq t_{hold}$
*   *Violation:* Occurs if the logic is too fast (the new data "catches up" to the clock edge too quickly).
*   *Fix:* Add buffers to increase the contamination delay. Note that *changing the clock speed does not fix hold time violations.*

---

## 4. Clock Skew
The time difference between the clock signal reaching two different flip-flops due to wire lengths and delays in the clock distribution network.

*   *Impact:* Skew effectively reduces the available time for logic, increasing the "sequencing overhead."
*   *Setup effect:* $T_c \geq t_{pcq} + t_{pd} + t_{setup} + t_{skew}$
*   *Hold effect:* $t_{ccq} + t_{cd} \geq t_{hold} + t_{skew}$

---

## 5. Verification Approaches
Verification ensures the design is both functionally correct and meets timing requirements.

### Functional Verification (Testbenches)
*   *Device Under Test (DUT):* The module being tested.
*   *Golden Model:* A high-level, bug-free behavioral model used to compare outputs.
*   *Types of Testbenches:*
    1.  *Simple:* Manual input and manual output checking (non-scalable).
    2.  *Self-Checking:* Manual input but automated output comparison.
    3.  *Automatic:* Automated input generation (random or sequential) and comparison against a Golden Model.

### Timing Verification
*   Performed using CAD tools (like Vivado or Synopsis).
*   *Static Timing Analysis (STA):* The tool checks all paths for violations without full simulation.
*   *Fixing Timing:* Often involves an iterative process of restructuring logic or adding registers (pipelining).

---

## 6. Design Principles for Timing
*   *Critical Path Design:* Focus on the longest path to determine the max frequency.
*   *Balanced Design:* Try to make all logic paths between registers roughly the same length to avoid "wasted" time in shorter paths.
*   *Optimize for the Common Case:* Ensure the most frequent operations are the fastest.
