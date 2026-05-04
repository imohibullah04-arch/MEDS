# Study Guide: Combinational Logic (Lecture 2)

## 1. The Core Philosophy: Why Boolean Algebra?
To build a computer, we need a way to translate human logic into electrical signals. *Boolean Algebra* is the bridge. It allows us to:
*   *Simplify:* Use fewer transistors to do the same job.
*   *Optimize:* Reduce the distance signals travel (lower latency).
*   *Automate:* Write software that designs the hardware for us.

### The Big Three Operations
*   *NOT $\bar{A}$:* The contrarian. If it's 1, it becomes 0.
*   *AND ($A \cdot B$):* The gatekeeper. It only says "Yes" if everyone agrees.
*   *OR ($A + B$):* The optimist. It says "Yes" if at least one person is on board.

---

## 2. Laws of the Land (Optimization Tools)
These aren't just math homework; they are recipes for saving money and power on a chip.

*   *De Morgan’s Laws:* These are the most famous. They allow you to swap between AND and OR gates just by flipping the "bubbles" (inversions). 
    *   Rule: Break the bar, change the sign.
*   *Duality:* Every Boolean identity has a "twin." If you swap all ANDs for ORs and all 1s for 0s, the statement remains true.



---

## 3. The Two Ways to Describe a Function
When looking at a Truth Table, you can describe it in two "languages":

1.  *Sum of Products (SOP):* You look only at the *successes* (where Output = 1). You create a list of all specific input combinations (Min terms) that yield a 1 and OR them together.
2.  *Product of Sums (POS):* You look at the *failures* (where Output = 0). You create constraints to avoid those zeros and AND them together.

---

## 4. The Functional Building Blocks
We rarely build processors gate-by-gate anymore. Instead, we use these "Lego bricks":

### The Decoder (The Pattern Detector)
If you have a 3-bit code (like 101), the decoder identifies it and turns on exactly one specific wire (Wire #5). 
*   *Uses:* Picking a specific address in memory or identifying an instruction.



### The Multiplexer / MUX (The Selector)
Think of this as a railroad switch. You have multiple data tracks, but only one can go through to the station. You use a "Select" signal to pick which one.
*   *Pro-Tip:* FPGAs use these as *Lookup Tables (LUTs)*. Instead of building a circuit, they just "look up" the answer in a pre-programmed table.



### The Full Adder
This is the heart of math. It takes two bits and a "carry-over" from a previous step, then spits out a *Sum* and a new *Carry*. By chaining these together, we can add numbers of any size.

---

## 5. The Real World: Power & Energy
Hardware isn't just math; it's physics. Every time a bit flips, it costs:
*   *Dynamic Power ($P \propto V^2$):* Power used during the "flip." Because Voltage is squared, cutting the voltage in half reduces your power consumption by four!
*   *Static Power:* The "leak." Even when your phone is in your pocket, transistors leak a tiny bit of current.

---

## 6. Moore’s Law & Innovation
*Moore’s Law* isn't a law of physics; it's an observation of economics. Gordon Moore realized we could double the number of transistors on a chip every two years by making them smaller. 
*   *The Bottom Line:* Smaller transistors are cheaper, faster, and allow for the complex AI systems we use today.