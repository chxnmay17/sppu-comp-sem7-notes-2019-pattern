
# Performance Measures of Multithreaded Algorithms

## 1. Speedup ($S$)
**Definition:** Speedup measures how much faster a parallel algorithm runs compared to its best sequential counterpart. It is the primary metric for evaluating the benefit of parallelization.

* **Formula:** $$S = \frac{T_1}{T_P}$$
    * $T_1$: Execution time on a single processor (Sequential work).
    * $T_P$: Execution time on $P$ processors.
* **Ideal Case:** Linear Speedup ($S = P$).
* **Actual Case:** Sub-linear (due to overhead and serial portions, governed by **Amdahl's Law**).

## 2. Efficiency ($E$)
**Definition:** Efficiency measures how effectively the utilized computing resources (processors) are being used. It quantifies the "return on investment" of adding more threads.

* **Formula:** $$E = \frac{S}{P} = \frac{T_1}{P \times T_P}$$
* **Range:** $0 < E \le 1$.
* **Interpretation:**
    * $E = 1$: Perfect utilization (rare).
    * $E < 0.5$: Poor utilization (processors are idling often).

## 3. Throughput
**Definition:** Throughput is the rate at which the system completes tasks or processes data units over a specific period.

* **Focus:** It emphasizes the **quantity** of work done rather than the speed of a single task.
* **Goal:** Maximize throughput (Jobs per second).
* **Relation:** Often, increasing concurrency improves throughput even if individual latency remains constant.
<img width="500" height="250" alt="image" src="https://github.com/user-attachments/assets/20e01b38-89a6-4cf0-8495-811f61b33601" />

## 4. Contention
**Definition:** Contention occurs when multiple threads try to access the same shared resource (lock, memory bus, cache line) simultaneously.

* **Effect:** One thread succeeds, while others must **wait** or **retry**.
* **Impact:** High contention acts as a bottleneck, serializing execution and drastically reducing Speedup.
* **Keywords:** Resource Starvation, Lock Granularity, False Sharing.
<img width="400" height="208" alt="image" src="https://github.com/user-attachments/assets/c28af652-1e72-407f-a694-a78f71b33816" />

## 5. Latency
**Definition:** Latency is the elapsed time from the start of a single task to its completion.

* **Focus:** It emphasizes the **speed** of a single operation (Response Time).
* **Goal:** Minimize latency (Seconds per Job).
* **Trade-off:** Sometimes, techniques to improve throughput (like batching) negatively impact latency.

---

## 6. Visual Representation: Speedup vs. Contention

The diagram below shows how adding threads ideally improves performance (Linear Speedup) versus reality (Contention/Overhead).



```mermaid
graph TD
    subgraph "Performance Metrics"
    Start[start] --> T1[Sequential Time T1]
    T1 -->|Parallelize| TP[Parallel Time TP]
    
    TP --> Calc{Calculate Metrics}
    
    Calc -->|T1 / TP| Speed[Speedup]
    Speed -->|Speed / P| Eff[Efficiency]
    
    TP -->|High Overhead| Contention[Contention Issues]
    Contention -->|Reduces| Speed
    end

    style Speed fill:#ccffcc,stroke:#333,color:#000
    style Eff fill:#e6f3ff,stroke:#333,color:#000
    style Contention fill:#ffcccc,stroke:#333,color:#000
````

## Summary Table

| Measure | Formula / Concept | Goal |
| :--- | :--- | :--- |
| **Speedup** | $T_1 / T_P$ | Maximize (Close to $P$) |
| **Efficiency** | $Speedup / P$ | Maximize (Close to 1) |
| **Throughput** | Jobs / Time | Maximize |
| **Contention** | Resource Conflict | Minimize |
| **Latency** | Time / Job | Minimize |

```
```
