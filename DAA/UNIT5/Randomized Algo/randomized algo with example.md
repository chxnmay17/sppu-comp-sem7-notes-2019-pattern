
# Randomized Algorithms

## 1. Definition
A **Randomized Algorithm** is an algorithm that employs a degree of randomness as part of its logic. Unlike deterministic algorithms, it uses a random number generator to make decisions at specific steps, meaning the execution flow or the output can vary even for the same input.

* **Core Principle:** `Output = Logic + Random Bit Stream`
* **Goal:** To simplify the algorithm or improve the **Average-Case Time Complexity**, avoiding worst-case scenarios constructed by an adversary.

---

## 2. Categories of Randomized Algorithms

| Type | Output Correctness | Running Time | Example |
| :--- | :--- | :--- | :--- |
| **Las Vegas** | **Always Correct** | Random (Variable) | Randomized QuickSort |
| **Monte Carlo** | **Probably Correct** (with high probability) | Deterministic (Fixed) | Karger’s Min-Cut |

---

## 3. Suitable Example: Randomized QuickSort

**Problem:** Standard QuickSort uses the first or last element as the pivot. If the input array is already sorted, the time complexity degrades to **$O(n^2)$**.

**Randomized Solution:**
Instead of picking a fixed pivot, we select the pivot **randomly** from the subarray.
1.  **Step 1:** Select a random index $r$ in the range $[low, high]$.
2.  **Step 2:** Swap $Arr[r]$ with $Arr[high]$.
3.  **Step 3:** Use $Arr[high]$ as the pivot and partition normally.

**Result:**
By shuffling the pivot choice, we destroy the specific patterns (like sorted arrays) that cause worst-case behavior. The expected time complexity becomes **$O(n \log n)$** with very high probability.

---

## 4. Visual Representation: Flow Logic

The diagram below shows how the random source injects decision-making into the standard flow.

```mermaid
graph TD
    Start((Start)) --> Input[Input Array]
    Input --> Rand{Generate Random Index}
    
    Rand --> Pivot[Pick Random Pivot]
    Pivot --> Partition[Partition Array]
    
    Partition --> Left[Recurse Left]
    Partition --> Right[Recurse Right]
    
    Left --> Combine
    Right --> Combine
    Combine --> End((Sorted))

    style Rand fill:#ffcccc,stroke:#333,color:#000
    style Pivot fill:#ccffcc,stroke:#333,color:#000
````

## 5\. Key Advantages

  * **Simplicity:** Often easier to implement than complex deterministic algorithms (e.g., finding the true median for pivot).
  * **Efficiency:** Excellent average-case performance.
  * **Robustness:** Hard to give "bad inputs" that trigger worst-case performance.

<!-- end list -->

```
```
