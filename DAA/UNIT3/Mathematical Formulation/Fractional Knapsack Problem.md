# **Fractional Knapsack Problem — Mathematical Formulation**

### **1. Given**
* $n$ items
* Item $i$ has:
  * Profit/value: $p_i$
  * Weight: $w_i$
* Knapsack capacity: $W$

---

### **2. Decision Variable**
$$x_i = \text{fraction of item } i \text{ included in the knapsack}$$

$$0 \le x_i \le 1$$

---

### **3. Objective Function (Maximize Total Profit)**
$$\max Z = \sum_{i=1}^{n} p_i x_i$$

---

### **4. Constraint (Weight Limit)**
$$\sum_{i=1}^{n} w_i x_i \le W$$

---

### **5. Boundary Conditions**
$$0 \le x_i \le 1 \quad \forall i$$

---

# **Complete Mathematical Model**

$$
\begin{aligned}
\text{Maximize } & Z = \sum_{i=1}^{n} p_i x_i \\
\text{subject to } & \sum_{i=1}^{n} w_i x_i \le W, \\
& 0 \le x_i \le 1 \quad \forall i.
\end{aligned}
$$

---

# **Diagram**

```text
      Items
   ┌───────────┬──────────┬──────────┐
   │   Item i  │  pi      │  wi      │
   └───────────┴──────────┴──────────┘
          ↓ Select fraction xi
          ↓ (0 ≤ xi ≤ 1)

        ┌──────────────────────────┐
        │        KNAPSACK          │
        │  Capacity = W            │
        │  Maximize Σ pi·xi        │
        └──────────────────────────┘
