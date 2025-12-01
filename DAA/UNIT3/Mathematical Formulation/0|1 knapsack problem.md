

### Mathematical Formulation: 0/1 Knapsack Problem

**Problem Statement:** Given a set of $n$ items, each with a specific weight and value, determine which items to include in a collection so that the total weight is less than or equal to a given limit and the total value is as large as possible.


---
#### 1. Notation and Parameters
Let there be $n$ items labeled $1$ to $n$.
* $v_i$: The **value** (or profit) of item $i$.
* $w_i$: The **weight** of item $i$.
* $W$: The maximum **weight capacity** of the knapsack.

---
#### 2. Decision Variable
We define a binary decision variable $x_i$ for each item $i$:

$$
x_i =
\begin{cases}
1 & \text{if item } i \text{ is selected} \\
0 & \text{otherwise}
\end{cases}
$$

---
#### 3. The Model

The problem can be modeled as the following Integer Linear Programming (ILP) problem:
**Maximize:**
$$Z = \sum_{i=1}^{n} v_i x_i$$


---
**Subject to (Constraints):**

1.  **Capacity Constraint:** The total weight of selected items must not exceed the knapsack capacity.
    $$\sum_{i=1}^{n} w_i x_i \leq W$$

2.  **Binary Constraint:** An item is either completely included or completely excluded (cannot be broken fractionally).
    $$x_i \in \{0, 1\} \quad \text{for } i = 1, 2, \dots, n$$

---

### Key Technical Notes
* **Combinatorial Optimization:** This is a classic optimization problem seeking a global maximum.
* **NP-Complete:** The 0/1 Knapsack problem is NP-complete. Unlike the *Fractional Knapsack* problem (which allows $0 \leq x_i \leq 1$ and is solvable by a Greedy approach), the 0/1 variant usually requires **Dynamic Programming** or **Branch and Bound** methods to solve efficiently.
* **Feasible Region:** The constraints define the feasible region; the objective function $Z$ searches for the optimal point within that discrete region.

***

