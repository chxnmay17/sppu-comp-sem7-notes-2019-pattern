<img width="565" height="76" alt="image" src="https://github.com/user-attachments/assets/661f3680-a481-4672-aa93-be1069e0f4fa" />

# Potential Function Method (Amortized Analysis)

## 1. Definition: Potential Method
The **Potential Method** (also known as the Physicist's Method) is a technique for amortized analysis where we define a "potential energy" associated with the state of a data structure. This potential is used to pay for future expensive operations.

### Core Concept
* **Potential Function ($\Phi$):** We define a function $\Phi$ that maps a data structure state $D_i$ to a real number $\Phi(D_i)$ (the potential).
* **The Formula:** The amortized cost $\hat{c}_i$ of the $i$-th operation is defined as:
    $$\hat{c}_i = c_i + \Phi(D_i) - \Phi(D_{i-1})$$
    Where:
    * $c_i$: Actual cost of the operation.
    * $\Phi(D_i) - \Phi(D_{i-1})$: The change in potential.

### Validity Condition
For the analysis to be valid, we require that for all $n$, $\Phi(D_n) \ge \Phi(D_0)$. Usually, we define $\Phi(D_0) = 0$ and ensure $\Phi(D_i) \ge 0$. This ensures the total amortized cost is an upper bound on the total actual cost.

---

## 2. Illustration: Stack Operations (Push, Pop, Multipop)

**Goal:** Find the amortized cost of stack operations using the Potential Method.

### A. Define the Potential Function
Let $D_i$ be the state of the stack after the $i$-th operation. We define the potential function as the **number of items in the stack**:
$$\Phi(D_i) = \text{number of items in } D_i$$

* Start (Empty Stack): $\Phi(D_0) = 0$.
* Since stack size is never negative, $\Phi(D_i) \ge 0$ holds true.

### B. Analysis of PUSH(S, x)
* **Actual Cost ($c_i$):** $1$ (Inserting 1 item).
* **Change in State:** The stack size increases by 1.
    $$\Phi(D_i) - \Phi(D_{i-1}) = (s + 1) - s = 1$$
* **Amortized Cost ($\hat{c}_i$):**
    $$\hat{c}_{push} = c_i + \Delta \Phi = 1 + 1 = 2$$

### C. Analysis of POP(S)
* **Actual Cost ($c_i$):** $1$ (Removing 1 item).
* **Change in State:** The stack size decreases by 1.
    $$\Phi(D_i) - \Phi(D_{i-1}) = (s - 1) - s = -1$$
* **Amortized Cost ($\hat{c}_i$):**
    $$\hat{c}_{pop} = c_i + \Delta \Phi = 1 + (-1) = 0$$

### D. Analysis of MULTIPOP(S, k)
Let $k'$ be the actual number of items popped (where $k' = \min(k, s)$).
* **Actual Cost ($c_i$):** $k'$ (The loop runs $k'$ times).
* **Change in State:** The stack size decreases by $k'$.
    $$\Phi(D_i) - \Phi(D_{i-1}) = (s - k') - s = -k'$$
* **Amortized Cost ($\hat{c}_i$):**
    $$\hat{c}_{multipop} = k' + (-k') = 0$$

---

## 3. Visual Interpretation

The diagram below illustrates how the potential works. PUSH operations are "charged" extra (cost 2). This extra charge is stored as potential energy (height). POP operations are "free" (cost 0) because they consume the stored potential.



[Image of state space tree diagram]


```mermaid
graph TD
    subgraph "Phase 1: Accumulating Potential"
    Push1["PUSH (Actual: 1)"] -->|"Amortized Cost: 2"| State1["Stack Size: 1<br>Potential: 1"]
    State1 --> Push2["PUSH (Actual: 1)"]
    Push2 -->|"Amortized Cost: 2"| State2["Stack Size: 2<br>Potential: 2"]
    end

    subgraph "Phase 2: Releasing Potential"
    State2 --> Multi["MULTIPOP(2) (Actual: 2)"]
    Multi -->|"Uses Potential (-2)"| State3["Stack Size: 0<br>Potential: 0"]
    State3 -->|"Amortized Cost: 0"| End((Result))
    end

    style Push1 fill:#ccffcc,stroke:#333,color:#000
    style Push2 fill:#ccffcc,stroke:#333,color:#000
    style Multi fill:#ffcccc,stroke:#333,color:#000
    style State1 fill:#e6f3ff,stroke:#333,color:#000
    style State2 fill:#e6f3ff,stroke:#333,color:#000
    style State3 fill:#e6f3ff,stroke:#333,color:#000
````

-----

## 4\. Conclusion

Using the Potential Method, we determined the amortized costs:

| Operation | Actual Cost ($c_i$) | Amortized Cost ($\hat{c}_i$) |
| :--- | :--- | :--- |
| **PUSH** | $1$ | **$2$ ($O(1)$)** |
| **POP** | $1$ | **$0$ ($O(1)$)** |
| **MULTIPOP** | $\min(k, s)$ | **$0$ ($O(1)$)** |

Thus, the amortized cost of each operation is **$O(1)$**, and the total cost for a sequence of $n$ operations is **$O(n)$**.

---
# Potential Function Method of Amortized Analysis  
*(With stack example: PUSH, POP, MULTIPOP – exam-ready)*

---

## 1. What Is the Potential Function Method?

### Definition

The **Potential Method** (also called the *Physicist’s Method*) is a technique of **amortized analysis** in which we associate a **numeric potential** with the **state of a data structure**.

- Let the state after the *i-th* operation be \( D_i \).
- Define a **potential function**:
  
  $$
  \Phi(D_i) \ge 0
  $$

- The **amortized cost** of the *i-th* operation is:

  $$
  \hat{c}_i = c_i + \Phi(D_i) - \Phi(D_{i-1})
  $$

  where:
  - \( c_i \) = actual cost of the *i-th* operation  
  - \( \Phi(D_i) \) = potential after operation *i*  
  - \( \Phi(D_{i-1}) \) = potential before operation *i*  

### Key Idea (Technical)

> Potential represents **“stored work”** or **“energy”** in the data structure that can be used to pay for future operations.

**Technical Keywords:** potential function, amortized cost, stored credit, data structure state, non-negative potential.

---

## 2. Stack Operations Example (PUSH, POP, MULTIPOP)

We consider a stack supporting:

- `PUSH(x)` → push element x onto the stack  
- `POP()` → remove top element (if stack not empty)  
- `MULTIPOP(k)` → pop up to k elements or until stack becomes empty  

Assume **actual cost** of each individual POP or PUSH = 1 unit.

---

## 3. Choice of Potential Function

Let:

- \( s_i \) = number of elements in the stack after operation \( i \)

Define the **potential function**:

$$
\Phi(D_i) = s_i
$$

i.e., the potential is equal to the **number of elements currently in the stack**.

This is valid because:

- \( \Phi(D_i) \ge 0 \) for all i (non-negative)  
- \( \Phi(D_0) = 0 \) when stack is initially empty  

---

## 4. Amortized Cost of PUSH, POP, MULTIPOP

We now compute amortized costs using:

$$
\hat{c}_i = c_i + \Phi(D_i) - \Phi(D_{i-1})
$$

---

### 4.1 PUSH Operation

- Actual cost: \( c_i = 1 \) (one element pushed)
- Stack size increases by 1:

  $$
  s_i = s_{i-1} + 1
  $$

- Change in potential:

  $$
  \Phi(D_i) - \Phi(D_{i-1}) = s_i - s_{i-1} = 1
  $$

- Amortized cost:

  $$
  \hat{c}_i = c_i + \Phi(D_i) - \Phi(D_{i-1})
  = 1 + 1 = 2
  $$

So, **amortized cost of PUSH is O(1)**.

---

### 4.2 POP Operation

Assume the stack is non-empty.

- Actual cost: \( c_i = 1 \)
- Stack size decreases by 1:

  $$
  s_i = s_{i-1} - 1
  $$

- Change in potential:

  $$
  \Phi(D_i) - \Phi(D_{i-1}) = s_i - s_{i-1} = -1
  $$

- Amortized cost:

  $$
  \hat{c}_i = c_i + \Phi(D_i) - \Phi(D_{i-1})
  = 1 + (-1) = 0
  $$

So, **amortized cost of POP is O(1)** (even 0 in this analysis).

---

### 4.3 MULTIPOP(k) Operation

`MULTIPOP(k)` pops up to k elements or until the stack becomes empty.

Let:

- Before operation: stack has \( t \) elements.  
- Then, actual number of elements popped = \( p = \min(k, t) \).

- Actual cost:  
  $$ c_i = p $$  
  (each pop costs 1 unit)

- Stack size decreases by p:

  $$
  s_i = s_{i-1} - p
  $$

- Change in potential:

  $$
  \Phi(D_i) - \Phi(D_{i-1}) = s_i - s_{i-1} = -p
  $$

- Amortized cost:

  $$
  \hat{c}_i = c_i + \Phi(D_i) - \Phi(D_{i-1})
  = p + (-p) = 0
  $$

Thus, **amortized cost of MULTIPOP is also O(1)**.

---

## 5. Total Cost Over a Sequence of n Operations

Let there be **n operations** (PUSH, POP, MULTIPOP) starting from an empty stack.

Total amortized cost:

$$
\sum_{i=1}^{n} \hat{c}_i
= \sum_{i=1}^{n} \left( c_i + \Phi(D_i) - \Phi(D_{i-1}) \right)
$$

This is a **telescoping sum**:

$$
\sum_{i=1}^{n} \hat{c}_i
= \sum_{i=1}^{n} c_i + \Phi(D_n) - \Phi(D_0)
$$

Since \( \Phi(D_n) \ge 0 \) and \( \Phi(D_0) = 0 \):

$$
\sum_{i=1}^{n} \hat{c}_i \ge \sum_{i=1}^{n} c_i
$$

Because each amortized cost is **O(1)**, the total actual cost:

$$
\sum_{i=1}^{n} c_i = O(n)
$$

So, **PUSH, POP, and MULTIPOP all have O(1) amortized time**, and any sequence of n operations takes **O(n)** total time.

---

## 6. Small Diagram (Stack Size vs Operations)

```text
Stack size (Φ = number of elements)

^
|          PUSH      PUSH       MULTIPOP(3)
|           ▲         ▲             ▼▼▼
|           |         |             |
|      3 ───●─────────●─────────────●────
|      2 ───●─────────●─────────────●────
|      1 ───●─────────●─────────────●────
|      0 ───●─────────●─────────────●──────> Operations →
        Start     PUSH x       MULTIPOP(k)

Potential increases with PUSH,
decreases with POP / MULTIPOP,
paying for their actual cost.
````

---

## 7. Exam-Ready Summary

* **Potential Function Method**:

  * Uses a function ( \Phi(D_i) ) to measure stored “energy” in the data structure.
  * Amortized cost:
    $$ \hat{c}*i = c_i + \Phi(D_i) - \Phi(D*{i-1}) $$
* For a **stack** with potential = number of elements:

  * PUSH: amortized cost = 2 → **O(1)**
  * POP: amortized cost = 0 → **O(1)**
  * MULTIPOP(k): amortized cost = 0 → **O(1)**
* Any sequence of n operations (PUSH, POP, MULTIPOP) takes **O(n)** actual time.

This demonstrates how the **Potential Method** proves **constant amortized time** for stack operations.

---



