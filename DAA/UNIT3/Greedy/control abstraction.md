

<img width="883" height="82" alt="image" src="https://github.com/user-attachments/assets/22e435af-b8b5-4962-807a-449cb773d1f7" />


## **1. Meaning of Control Abstraction**
A control abstraction is a generic procedure (algorithm template) that outlines the structure of a specific algorithmic strategy.
It separates *how the greedy choice is made* from *how the algorithm is controlled*.




---

# **Control Abstraction for Greedy Method**

### **1. Idea (Concept)**

The **greedy method** builds a solution in **stages**, making at each stage a **locally optimal (greedy) choice** with respect to some **greedy criterion**, hoping to obtain a **globally optimal solution**.

---

### **2. Control Abstraction (Generic Greedy Algorithm)**

We define the following abstract functions:

* `Select(...)` → chooses the **next candidate** according to the **greedy criterion**
* `Feasible(S, x)` → checks if adding `x` to **current solution** `S` keeps it **feasible**
* `Solution(S)` → tests whether `S` is a **complete solution**
* `Objective(S)` → computes the **value** (cost/profit) of solution `S`
---

### **3. Pseudocode: Control Abstraction for Greedy Method**

```text
Greedy(A)   // A: set or list of candidates
{
    S = ∅                         // S: current solution (initially empty)

    while ( not Solution(S) )     // while solution not complete
    {
        x = Select(A)             // select best candidate according to greedy criterion

        if ( Feasible(S, x) )     // check if adding x is allowed (constraints satisfied)
            S = S ∪ { x }         // include x in the solution

        A = A − { x }             // remove x from further consideration
    }

    return S;                     // S is the greedy solution
}
```

**Keywords:** greedy criterion, locally optimal choice, feasible solution, candidate set, objective function.



---

## **3. Flow Diagram (Simple)**

```text
         ┌───────────────────────────┐
         │     Start: S = ∅, A       │
         └────────────┬──────────────┘
                      │
                      v
             ┌─────────────────┐
             │  Solution(S)?   │
             └───────┬─────────┘
                     │ No
                     v
             ┌─────────────────┐
             │   x = Select(A) │
             └───────┬─────────┘
                     v
             ┌────────────────────────┐
             │   Feasible(S, x) ?     │
             └───────┬───────────────┘
                 No  │   Yes
                     v
              (skip x)      ┌────────────────┐
                            │  S = S ∪ {x}   │
                            └────────────────┘
                     (in both cases)
                             │
                             v
                    ┌─────────────────┐
                    │   A = A − {x}   │
                    └───────┬─────────┘
                            │
                            └──────► back to Solution(S)?
```

---



### **4. Time Complexity of the Control Abstraction**

Let:

* There be **n candidates** in `A`
* `Select(A)` takes time: ( T_{\text{select}} )
* `Feasible(S, x)` takes time: ( T_{\text{feasible}} )
* `Solution(S)` takes time: ( T_{\text{solution}} )

#### **Number of calls (worst case)**

* `Select` is called at most **n** times
* `Feasible` is called at most **n** times
* `Solution` is checked in each iteration → at most **n + 1** times

#### **Overall time complexity (abstract form)**

$$
T(n) = O\big(n \cdot (T_{\text{select}} + T_{\text{feasible}} + T_{\text{solution}})\big)
$$

* If each of these operations is **(O(1))**, then:
  $$T(n) = O(n)$$
* In many practical greedy algorithms, there is an initial **sorting step** (e.g., sorting items by ratio), which takes:
  $$O(n \log n)$$
  and this often **dominates** the running time.

---

### **5. Comment (Exam-style)**

* The **control abstraction** of the greedy method specifies **how** the algorithm proceeds:

  * repeatedly **selecting** the best candidate (locally optimal),
  * checking **feasibility**, and
  * **extending** the current solution
* The **exact time complexity** depends on the implementation of `Select`, `Feasible`, and `Solution`,
  but is generally **polynomial**, often ( O(n \log n) ) due to sorting or data structure operations.

---


