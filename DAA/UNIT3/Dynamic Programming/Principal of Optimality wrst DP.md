<img width="870" height="69" alt="image" src="https://github.com/user-attachments/assets/e50e4aa2-8cdc-4b5f-ac5b-ce21dd806cb1" />


---

# **Principle of Optimality (Dynamic Programming)**

### **Definition**

The **Principle of Optimality**, given by **Richard Bellman**, states:

> *“An optimal solution to a problem contains within it optimal solutions to its subproblems.”*

---

# **1. Meaning (Pointwise & Technical)**

1. A problem is broken into **overlapping subproblems**.
2. If the **overall (global) solution** is optimal,
   then **each subproblem solution must also be optimal**.
3. No optimal solution can contain a **non-optimal** solution inside it.
4. This principle is the basis of **Dynamic Programming (DP)**.

---

# **2. Mathematical Representation**

Suppose a problem starts in state $S$ and consists of stages.

Let:

* $f(S)$ = optimal value (cost/profit) from initial state $S$
* $S'$ = next state derived by choosing decision $d$
* $g(S, d)$ = cost/value of decision $d$ at state $S$

### **Bellman’s Optimality Equation**

$$
f(S) = \max_{d \in D(S)} \left[, g(S, d) + f(S') ,\right]
$$

or for minimization problems:

$$
f(S) = \min_{d \in D(S)} \left[, g(S, d) + f(S') ,\right]
$$
$$
f(S) = \min_{d \in D(S)} \left[\, g(S, d) + f(T(S, d)) \,\right]
$$

This states that:

> **The optimal value at state $S$ equals the best immediate decision plus the optimal value of the next state.**

---

# **3. Small Diagram**

```text
      Problem (State S)
              │
      ┌───────┴────────┐
      │                │
 Decision d1        Decision d2
      │                │
  Next State S1     Next State S2
      │                │
 Optimal f(S1)      Optimal f(S2)
      └───────┬────────┘
              │
        Choose the better
     f(S) = max{ f(S1), f(S2) }
```

---

# **4. Summary (Exam-ready)**

* DP works because **optimal solutions are built from optimal subsolutions**.
* The Principle of Optimality guarantees correctness of DP recurrence.
* Represented using **Bellman’s equation**.

---


