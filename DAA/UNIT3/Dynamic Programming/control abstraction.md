
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

<img width="497" height="813" alt="image" src="https://github.com/user-attachments/assets/72c5c6d7-158c-4cab-ab7e-2124c17aa639" />

---
<img width="419" height="252" alt="image" src="https://github.com/user-attachments/assets/76f9a1ef-fb1c-49b9-b5e9-8b8abdfefa64" />


---



<img width="734" height="376" alt="image" src="https://github.com/user-attachments/assets/234ded59-9545-4ceb-8d09-940881e62a2e" />
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







