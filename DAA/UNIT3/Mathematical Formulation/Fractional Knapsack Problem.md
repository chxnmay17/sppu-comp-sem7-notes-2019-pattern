
---
### Mathematical Formulation: Fractional Knapsack Problem

**Problem Statement:** Given a set of $n$ items, each with a specific weight and value, determine the fraction of each item to include in a collection so that the total weight is less than or equal to a given limit $W$, and the total value is maximized. Unlike the 0/1 variant, items can be broken down (divisible).


---
#### 1. Notation and Parameters
Let there be $n$ items labeled $1$ to $n$.
* $v_i$: The **value** (or profit) of item $i$.
* $w_i$: The **weight** of item $i$.
* $W$: The maximum **weight capacity** of the knapsack.

---
#### 2. Decision Variable
We define a continuous decision variable $x_i$ representing the **fraction** of item $i$ selected:

$$0 \leq x_i \leq 1$$

* If $x_i = 1$, the item is completely taken.
* If $x_i = 0$, the item is left behind.
* If $0 < x_i < 1$, a portion of the item is taken.

---
#### 3. The Model
The problem is modeled as a Linear Programming (LP) problem:

**Maximize (Objective Function):**
$$Z = \sum_{i=1}^{n} v_i x_i$$

---
**Subject to (Constraints):**

1.  **Capacity Constraint:** The sum of the weights of the fractions of selected items cannot exceed the capacity.
    $$\sum_{i=1}^{n} w_i x_i \leq W$$

2.  **Range Constraint:** The fraction taken must be between 0 and 1 inclusive.
    $$0 \leq x_i \leq 1 \quad \text{for } i = 1, 2, \dots, n$$

---

### Key Technical Notes

* **Greedy Property:** Unlike the 0/1 Knapsack problem (which requires Dynamic Programming), the Fractional Knapsack problem satisfies the **greedy choice property**.
* **Optimal Substructure:** An optimal solution to the problem contains within it optimal solutions to sub-problems.
* **Solution Strategy:** The problem is efficiently solved by sorting items based on their **value-per-unit-weight ratio** ($r_i = v_i / w_i$) in descending order and filling the knapsack.
* **Time Complexity:** The solving time is dominated by the sorting step, which is $O(n \log n)$.

***

