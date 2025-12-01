
<img width="1337" height="120" alt="image" src="https://github.com/user-attachments/assets/95630fe0-9c2a-4c9b-9b78-1ced620ccdbc" />

# **Control Abstraction for Dynamic Programming (Using Fibonacci Numbers)**

## **Definition:**

The control abstraction for **Dynamic Programming (DP)** outlines the mechanism of solving a complex problem by:

* Breaking it into **overlapping subproblems**
* Solving each subproblem **only once**
* **Storing** the result in a table (**memoization** or **tabulation**) so that future subproblems can **reuse** previously computed values.

We illustrate this using the **Fibonacci number computation**.


---
## **1. Components of the DP Control Abstraction**

1. **Define Subproblems**
   Identify a set of *subproblems* whose optimal solutions build the final solution.

2. **Determine State Variables**
   Represent each subproblem using *state parameters*.

3. **Establish Recurrence Relation**
   Express optimal value of a subproblem in terms of smaller subproblems.

4. **Compute Subproblems in Bottom-Up Order**
   Fill a **DP table** iteratively to ensure that solutions to smaller subproblems are already available.

5. **Construct Final Solution**
   The last-filled entry (usually `DP[n]` or `DP[n][m]`) gives the optimal solution.


---

## **1. Fibonacci Problem as a DP Example**

**Problem:** Compute the $n$-th Fibonacci number.

**Mathematical Recurrence:**

$$
F(n) =
\begin{cases}
0, & \text{if } n = 0 \\
1, & \text{if } n = 1 \\
F(n-1) + F(n-2), & \text{if } n \ge 2
\end{cases}
$$

This has:

* **Overlapping subproblems:** $F(n-1), F(n-2), F(n-3), \dots$
* **Optimal substructure:** $F(n)$ is **completely determined** by $F(n-1)$ and $F(n-2)$.

---

## **2. Control Abstraction (Top-Down DP / Memoization for Fibonacci)**

### **Algorithm `Fib_DP(n)`**

```text
Algorithm Fib_DP(n)
Input : n  (index of Fibonacci number)
Output: F(n)

if n == 0 or n == 1 then
      return n                          // Base case: F(0)=0, F(1)=1

if Table[n] is already computed then
      return Table[n]                   // Lookup Step (Memoization)

else
      x ← Fib_DP(n - 1)                 // Solve subproblem F(n-1)
      y ← Fib_DP(n - 2)                 // Solve subproblem F(n-2)
      Table[n] ← x + y                  // Store Step: F(n) = F(n-1) + F(n-2)
      return Table[n]
````

### **Technical Keywords:**

overlapping subproblems, memoization, lookup step, store step, recurrence relation, base case, subproblem reuse.

---

## **3. Equivalent Bottom-Up (Tabulation) Control Abstraction for Fibonacci**

```text
Algorithm Fib_DP_BottomUp(n)
Input : n
Output: F(n)

create array F[0..n]

F[0] ← 0
if n ≥ 1 then
      F[1] ← 1

for i ← 2 to n do
      F[i] ← F[i-1] + F[i-2]            // DP transition using smaller subproblems

return F[n]
```

Here:

* `F[i]` is the **DP table entry** for subproblem ( F(i) ).
* Each `F[i]` is computed **once**, using already computed `F[i-1]` and `F[i-2]`.

---

## **4. Small Diagram (DP Table for Fibonacci)**

```text
   i :      0     1     2     3     4     5    ...    n
        ┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
F[i] =  │ F0  │ F1  │ F2  │ F3  │ F4  │ F5  │ ... │ Fn  │
        └─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
          0     1   F1+F0 F2+F1 F3+F2  ...   F(n-1)+F(n-2)
```

Or as a **subproblem dependency**:

```text
          F(n)
         /    \
      F(n-1)  F(n-2)
       /  \      /  \
   F(n-2) F(n-3) ...
(Computed once and stored in Table)
```

---

## **5. Time Complexity of This DP Abstraction (Using Fibonacci)**

### **Top-Down with Memoization (Fib_DP):**

* Each value `F(k)` for `0 ≤ k ≤ n` is computed **once** and stored in `Table[k]`.
* Each computation of `F(k)` does **O(1)** work (just an addition and a few checks).

Therefore:

$$
T(n) = O(n)
$$

### **Bottom-Up (Fib_DP_BottomUp):**

* The loop runs from `2` to `n` → `(n - 1)` iterations.
* Each iteration performs **O(1)** work.

Therefore:

$$
T(n) = O(n)
$$

<img width="1034" height="476" alt="image" src="https://github.com/user-attachments/assets/234ded59-9545-4ceb-8d09-940881e62a2e" />
<img width="704" height="237" alt="image" src="https://github.com/user-attachments/assets/459a8aba-73ab-4987-b7a0-39f1e595064e" />

### **Space Complexity:**

* Using a table `F[0..n]`: space = **O(n)**.
* With optimization (keeping only last two values): space can be reduced to **O(1)**.

---

## **6. Comment (Exam-Style Conclusion)**

* The **control abstraction** for DP, illustrated by the Fibonacci example, shows:

  * **Subproblem decomposition:** compute all `F(k)` for `k ≤ n`
  * **Result storage:** use `Table[k]` to **avoid recomputation**
  * **Bottom-up or top-down** evaluation using the **same recurrence**
  * For Fibonacci, this abstraction reduces time from **exponential** (naive recursion) to **linear**:

  
$$
  T(n) = O(n)
  $$

This clearly demonstrates how **Dynamic Programming** transforms a recursive specification into an efficient algorithm.

Below is the **university-expected**, **pointwise**, **technical**, **formatted** Markdown answer with a **small diagram** and **time-complexity explanation**.

---







