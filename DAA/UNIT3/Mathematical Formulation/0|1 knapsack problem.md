
---

# **0/1 Knapsack Problem — Mathematical Formulation**

### **1. Given**

* $n$ items
* Item $i$ has:

  * Profit/value: $p_i$
  * Weight: $w_i$
* Knapsack capacity: $W$

---

### **2. Decision Variable**

$$
x_i =
\begin{cases}
1, & \text{if item } i \text{ is included} \
0, & \text{if item } i \text{ is not included}
\end{cases}
$$

---

### **3. Objective Function (Maximize Total Profit)**

$$
\max Z = \sum_{i=1}^{n} p_i x_i
$$

---

### **4. Constraint (Weight Limit)**

$$
\sum_{i=1}^{n} w_i x_i \le W
$$

---

### **5. Binary Condition**

$$
x_i \in {0,1} \quad \forall i
$$

---

# **Complete Mathematical Model**

$$
\begin{aligned}
\text{Maximize } \quad & Z = \sum_{i=1}^{n} p_i x_i \
\text{subject\ to } \quad
& \sum_{i=1}^{n} w_i x_i \le W, \
& x_i \in {0,1} \quad \forall i.
\end{aligned}
$$

---

# **Diagram**

```text
      Items
   ┌───────────┬──────────┬──────────┐
   │   Item i  │  p_i     │  w_i     │
   └───────────┴──────────┴──────────┘
          ↓ Choose x_i ∈ {0,1}
          ↓

        ┌──────────────────────────┐
        │        KNAPSACK          │
        │     Capacity = W         │
        │   Maximize Σ p_i·x_i     │
        │   No fractions allowed   │
        └──────────────────────────┘
```

---


