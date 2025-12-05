<img width="511" height="43" alt="image" src="https://github.com/user-attachments/assets/8a9a8ce2-c50a-4b19-9485-4b5d4993ab9d" />
8mrks
# Methods of Amortized Analysis

## 1. Definition
**Amortized Analysis** guarantees the average performance of each operation in the worst-case sequence of operations. Unlike average-case analysis (which relies on probability), amortized analysis ensures that the total cost of a sequence of $n$ operations is bounded by $T(n)$, yielding an amortized cost of $T(n)/n$ per operation.

---

## 2. Methods of Amortized Analysis

There are three primary methods to perform amortized analysis:

### A. Aggregate Analysis
* **Concept:** This is the brute-force summation method. We calculate the total cost $T(n)$ for a sequence of $n$ operations in the worst case and divide by $n$.
* **Formula:**
    $$\text{Amortized Cost} = \frac{\text{Total Cost of Sequence}}{\text{Number of Operations}}$$
* **Characteristic:** It assigns the same amortized cost to every operation type.

### B. Accounting Method (The Banker's Method)
* **Concept:** We assign specific **amortized costs** (charges) to different operations.
    * If Amortized Cost > Actual Cost, the surplus is stored as **Credit** (or savings) on specific elements in the data structure.
    * If Amortized Cost < Actual Cost, we use the stored credit to pay for the operation.
* **Condition:** The total amortized cost must always be greater than or equal to the total actual cost.
  ```math
  \sum_{i=1}^{n} \hat{c}_i \ge \sum_{i=1}^{n} c_i
  ```

### C. Potential Method (The Physicist's Method)
* **Concept:** Instead of storing credit on specific elements, we define a "potential energy" for the entire data structure state.
* **Function:** We define a potential function $\Phi(D_i)$ that maps state $D_i$ to a real number.
* **Formula:** The amortized cost $\hat{c}_i$ of the $i$-th operation is:
```math
\hat{c}_i = c_i + \Phi(D_i) - \Phi(D_{i-1})
```

*(Actual Cost + Change in Potential)*

---

## 3. Suitable Example: Dynamic Array (Vector) Resizing

**Problem:** Inserting elements into a dynamic array.
* **Normal Insert:** Cost = $1$ (if space exists).
* **Resize Insert:** Cost = $k$ (if array is full, allocate new size $2k$, copy $k$ elements).

### Applying Aggregate Analysis
1.  Assume we insert $n$ elements (where $n$ is a power of 2).
2.  **Actual Costs:**
    * Most inserts cost $1$.
    * Expansions occur at indices 1, 2, 4, 8, ..., $n$. Costs are 1, 2, 4, ..., $n$.
3.  **Total Cost Calculation:**
    $$T(n) = \sum \text{Normal Inserts} + \sum \text{Copying Costs}$$
    $$T(n) = n + (1 + 2 + 4 + \dots + n)$$
    $$T(n) = n + (2n - 1) \approx 3n$$
4.  **Amortized Cost:**
    $$\frac{3n}{n} = 3 = O(1)$$

### Applying Accounting Method
* **Goal:** We want to pay for the future expensive copying operation using cheaper current operations.
* **Strategy:** Charge **\$3** for every `Append` operation.
    * **\$1**: Pays for the actual insertion.
    * **\$1**: Stored as credit to move *this* element when the array doubles.
    * **\$1**: Stored as credit to move *another* (older) element that has already used its credit.
* **Result:** When the array doubles, we have enough credit (\$2 per element) to pay for the copying cost. The amortized cost is constant **$O(1)$**.

---

## 4. Visual Diagram: Accounting Method

The diagram below shows how charging \$3 covers the cost. The "coins" represent credits stored on elements.

```mermaid
graph TD
    subgraph "Element Insertion (Charge $3)"
    A[Insert Element] -->|Pays $1| B(Actual Work)
    A -->|Saves $2| C(Credit Bank)
    end
    
    subgraph "Array Doubling (Expensive)"
    D[Resize Event] -->|Needs Money| E{Check Credit}
    C -->|Pays for Copying| E
    E --> F[Operation Paid!]
    end

    style A fill:#e6f3ff,stroke:#333,color:#000
    style B fill:#ffffff,stroke:#333,color:#000
    style C fill:#ccffcc,stroke:#333,color:#000
    style D fill:#ffcccc,stroke:#333,color:#000
    style E fill:#ffffff,stroke:#333,color:#000
    style F fill:#ffffff,stroke:#333,color:#000
````

### Key Technical Keywords

  * **Worst-Case Sequence**
  * **Credit / Prepayment**
  * **Potential Function $\Phi$**
  * **Global Average**
  * **Upper Bound**

<!-- end list -->


# Methods of Amortized Analysis  
*(Clear, pointwise, technical keywords, small diagram, and suitable example – exam-ready)*

Amortized analysis determines the **average running time per operation** for a sequence of operations, even if some operations are expensive.  
It does **not** use probability; instead, it spreads the cost of expensive operations across many cheap ones.

---

# 1. Methods of Amortized Analysis

There are **three standard methods**:

1. **Aggregate Method**  
2. **Accounting Method**  
3. **Potential Method**

Each method derives the **amortized cost** in a different way.

---

# 2. Method 1: Aggregate Method

### Definition  
> Compute the **total cost** of a sequence of \( n \) operations and divide it equally among all operations.

Formally:
```

Total Cost = T(n)
Amortized Cost = T(n) / n

```

### Technical Keywords:
total cost, sequence analysis, equal amortized cost, upper bound.

---

# 3. Method 2: Accounting Method  
(Also called “Banker’s Method”)

### Definition  
> Assign each operation a fixed **amortized cost**.  
> Surplus cost is stored as **credit**, which can be used to pay for future expensive operations.

- Cheap operations are **overcharged**.  
- Expensive operations are **undercharged**, using saved credits.

### Technical Keywords:
credit, debit, amortized charge, stored credit, prepaid work.

---

# 4. Method 3: Potential Method  
(Also called “Physicist’s Method”)

### Definition  
> Define a **potential function** \( \Phi \) that maps the state of the data structure to a non-negative number representing “stored energy” or future work.

Amortized cost of operation \( i \):

$$
\hat{c}_i = c_i + \Phi_i - \Phi_{i-1}
$$

Where:  
- \( c_i \) = actual cost  
- \( \Phi_i \) = potential after operation  
- \( \Phi_{i-1} \) = potential before operation

### Technical Keywords:
potential function, stored energy, amortized cost formula, data structure state.

---

# 5. Suitable Example for All Three Methods  
### Example: Dynamic Array Doubling (Inserting n Items)

A dynamic array doubles its size whenever it becomes full.

---

## **Actual Costs:**
- Insertion normally costs: **1 unit**  
- When resizing: copying **k** elements costs **k units**

Copy sequence: 1, 2, 4, 8, …, n

---

# A. Aggregate Method for the Example

Total work:

```

Cost of inserting n items = n
Cost of resizing (copying): 1 + 2 + 4 + ... + n = 2n - 1

```

Total cost:
```

T(n) = n + (2n - 1) = 3n - 1

```

Amortized cost:
```

(3n - 1) / n ≈ 3  → O(1)

```

---

# B. Accounting Method for the Example

Assign each insertion **amortized cost = 3 units**:

- 1 unit → actual insertion  
- 2 units → saved as **credit**

Credits pay for future resizing:

- To copy 1 element, need 1 unit  
- To copy 2 elements, need 2 units  
- To copy 4 elements, need 4 units  

The credit stored is always enough to pay for copying during expansions.

Thus, amortized cost = **O(1)**.

---

# C. Potential Method for the Example

Define potential function:

```

Φ = number of elements in the array

````

Then:
- When inserting without resize:  
  potential increases by 1 → amortized cost remains constant  
- When resizing:
  potential jumps, but the increase is matched by earlier potential

Final amortized insertion cost = **O(1)**.

---

# 6. Small Diagram: Array Expansion

```text
Initial size = 1
[ _ ]

Insert 1 → OK

Insert 2 → Resize to 2
[ 1, 2 ]

Insert 3 → Resize to 4
[ 1, 2, 3, _ ]

Insert 5 → Resize to 8
[ 1, 2, 3, 4, 5, _ , _ , _ ]

Copies = 1 + 2 + 4 + 8 + ...
````

---

# 7. Final Exam-Ready Summary

* **Amortized analysis** evaluates the average cost of operations over a sequence.
* **Aggregate Method:** Compute total cost and divide by ( n ).
* **Accounting Method:** Assign amortized charges and store credits.
* **Potential Method:** Use a potential function to track stored energy.
* All three methods show that dynamic array insertion has **O(1)** amortized complexity.

---


