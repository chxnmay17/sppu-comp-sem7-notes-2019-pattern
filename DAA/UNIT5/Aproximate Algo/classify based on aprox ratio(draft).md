<img width="557" height="61" alt="image" src="https://github.com/user-attachments/assets/af4e4cc2-7159-4b57-b913-aee770f2e22a" />

# Approximation Algorithms

## 1. Definition
**Approximation Algorithms** are efficient (Polynomial Time) algorithms used to find approximate solutions to **NP-Hard Optimization Problems**. Since finding the exact global optimal solution for these problems is computationally intractable (takes exponential time), we accept a feasible solution that is "close enough" to the optimal.

* **Goal:** To guarantee that the solution found is within a specific factor of the true optimal solution.
* **Key difference from Heuristics:** Heuristics (like Greedy) do not guarantee the quality of the solution. Approximation algorithms provide a mathematical **Performance Guarantee**.

### The Approximation Ratio ($\rho(n)$)
The quality of an approximation algorithm is measured by its **Approximation Ratio** $\rho(n)$.
Let:
* $C$: Cost of solution produced by the algorithm.
* $C^*$: Cost of the optimal solution.

For **Minimization** problems:
$$\frac{C}{C^*} \le \rho(n)$$

For **Maximization** problems:
$$\frac{C^*}{C} \le \rho(n)$$

In both cases, $\rho(n) \ge 1$. The closer $\rho(n)$ is to 1, the better the algorithm.

---

## 2. Classification Based on Approximation Ratio

Approximation algorithms are classified based on how close their approximation ratio $\rho(n)$ can get to 1 and how the time complexity relates to the error tolerance ($\epsilon$).

### A. Constant Factor Approximation
* **Definition:** The approximation ratio is a fixed constant $\alpha$, independent of the input size $n$.
* **Constraint:** $\rho(n) \le \alpha$ where $\alpha > 1$.
* **Examples:**
    * **Vertex Cover:** Ratio $\rho = 2$.
    * **Metric TSP:** Ratio $\rho = 1.5$ (Christofides Algorithm).
    * **Load Balancing:** Ratio $\rho = 2$.

### B. Polynomial Time Approximation Scheme (PTAS)
* **Definition:** The algorithm takes an additional input $\epsilon > 0$ (error parameter) and produces a solution with ratio $(1 + \epsilon)$.
* **Time Complexity:** Polynomial in input size $n$, but can be **Exponential in $1/\epsilon$**.
    * *Example:* $O(n^{2/\epsilon})$. If $\epsilon$ is small (high accuracy), the algorithm becomes very slow.
* **Example:** Euclidean TSP, Knapsack.

### C. Fully Polynomial Time Approximation Scheme (FPTAS)
* **Definition:** This is the best class of approximation algorithms. It produces a solution with ratio $(1 + \epsilon)$.
* **Time Complexity:** Polynomial in **both** the input size $n$ **and** $1/\epsilon$.
    * *Example:* $O(n^2 \cdot \frac{1}{\epsilon})$. It remains efficient even for high accuracy.
* **Example:** Subset Sum Problem, Knapsack (using rounding).

### D. Logarithmic Factor Approximation
* **Definition:** The approximation ratio grows as a logarithmic function of the input size.
* **Constraint:** $\rho(n) = O(\log n)$.
* **Example:** **Set Cover Problem** ($\rho = \ln n$).

---

## 3. Visual Classification Hierarchy

The diagram below shows the hierarchy of approximation classes. **FPTAS** is the most desirable subset of **PTAS**, which is a subset of **Constant Factor**.

```mermaid
graph TD
    Root[Optimization Problems] --> APX[Constant Factor<br>e.g., Vertex Cover]
    APX --> Log[Logarithmic Factor<br>e.g., Set Cover]
    APX --> PTAS[PTAS<br>Poly in n, Exp in 1/ε]
    PTAS --> FPTAS[FPTAS<br>Poly in n AND 1/ε<br>Best Class]

    style Root fill:#ffffff,stroke:#333,stroke-width:2px,color:#000
    style APX fill:#e6f3ff,stroke:#333,stroke-width:2px,color:#000
    style Log fill:#ffcccc,stroke:#333,stroke-width:2px,color:#000
    style PTAS fill:#ccffcc,stroke:#333,stroke-width:2px,color:#000
    style FPTAS fill:#ffffcc,stroke:#333,stroke-width:2px,color:#000
````

## Summary Table

| Class | Approx Ratio $\rho(n)$ | Time Complexity | Example |
| :--- | :--- | :--- | :--- |
| **FPTAS** | $1 + \epsilon$ | Poly($n, 1/\epsilon$) | Knapsack |
| **PTAS** | $1 + \epsilon$ | Poly($n$), Exp($1/\epsilon$) | Euclidean TSP |
| **Constant** | Constant $k$ | Poly($n$) | Vertex Cover ($\rho=2$) |
| **Logarithmic** | $O(\ln n)$ | Poly($n$) | Set Cover |


# Approximation Algorithms  
*(Clear, pointwise, technical keywords, small diagram, exam-ready)*

---

# 1. What Are Approximation Algorithms?

### **Definition**
An **approximation algorithm** is an algorithm used to find **near-optimal solutions** for **NP-hard optimization problems**, where finding the exact optimal solution is computationally infeasible.

Instead of giving the optimal answer, it gives a solution that is **provably close** to the optimal.

### **Technical Keywords:**  
NP-hard, optimization, approximate solution, performance guarantee, approximation ratio, polynomial-time algorithm.

---

# 2. Why Approximation Algorithms?

- Many critical problems (TSP, Knapsack, Vertex Cover) are **NP-hard**.  
- Exact algorithms take **exponential time**.  
- Approximation algorithms run in **polynomial time** and deliver solutions that are:  
  - *Close to optimal*,  
  - *Fast*,  
  - *Mathematically guaranteed* to be within a specific bound.

---

# 3. Approximation Ratio (Performance Guarantee)

The **approximation ratio** measures how close the approximate solution is to the optimal solution.

Let:

- `OPT` = optimal solution value  
- `A` = solution returned by the approximation algorithm  

For **minimization problems**:

$$
\frac{A}{OPT} \le \alpha
$$

For **maximization problems**:

$$
\frac{OPT}{A} \le \alpha
$$

Here, **α ≥ 1** is the **approximation factor**.

### Interpretation:
- α = 1 → exact algorithm  
- α close to 1 → high-quality approximation  
- Larger α → poorer approximation

---

# 4. Classification of Approximation Algorithms  
*(Based on Approximation Ratio)*

---

## **1. Constant-Factor Approximation Algorithms**

### **Definition:**  
Achieve a **constant approximation ratio α**, independent of input size.

Examples:
- Vertex Cover: 2-approximation  
- Metric TSP: 1.5-approximation  
- Set Cover (greedy): ln(n)-approximation (almost constant)

### Formal:
$$
A \le \alpha \cdot OPT
$$

---

## **2. Logarithmic-Factor Approximation Algorithms**

Approximation ratio grows **logarithmically** with input size.

Examples:
- Set Cover → **O(log n)** approximation  
- Multicut problems

---

## **3. Polynomial-Factor Approximation Algorithms**

Approximation quality grows **polynomially** with input size.

Not very accurate, but still useful for extremely hard problems.

Examples:
- Approximations for some packing/scheduling problems.

---

## **4. PTAS (Polynomial-Time Approximation Scheme)**

### **Definition:**  
For any **ε > 0**, PTAS gives a solution within factor:

$$
(1 + \varepsilon)\text{ of optimal}
$$

Running time:  
Polynomial in `n`, but may be exponential in `1/ε`.

Example:  
- Knapsack PTAS  
- Euclidean TSP PTAS

---

## **5. FPTAS (Fully Polynomial-Time Approximation Scheme)**

### **Definition:**  
Improved version of PTAS where running time is polynomial in both:

- `n`  
- `1/ε`

Examples:
- Knapsack FPTAS  
- Some dynamic programming approximations

---

## **6. Randomized Approximation Algorithms**

Use randomization to improve approximation quality or running time.

Example:
- Randomized rounding in Linear Programming  
- MAX-CUT randomized 0.878-approximation

---

# 5. Small Diagram (Classification Overview)

```text
                Approximation Algorithms
                          ●
     --------------------------------------------------
     |          |             |          |            |
 Constant    Logarithmic   Polynomial   PTAS        FPTAS
  Ratio       Ratio           Ratio      |            |
  α-fixed     O(log n)        poly(n)    (1+ε)OPT   poly(n, 1/ε)
````

---

# 6. Final Exam-Ready Summary

* **Approximation algorithms** give **near-optimal solutions** for NP-hard problems in polynomial time.
* Quality is measured using the **approximation ratio**.
* Based on this ratio, they are classified as:

  * **Constant-factor** approximation
  * **Logarithmic-factor** approximation
  * **Polynomial-factor** approximation
  * **PTAS** (Polynomial-Time Approximation Scheme)
  * **FPTAS** (Fully Polynomial-Time Approximation Scheme)
  * **Randomized approximations**
* They provide fast, scalable, and mathematically guaranteed solutions for computationally hard optimization problems.

---
