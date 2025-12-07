<img width="473" height="31" alt="image" src="https://github.com/user-attachments/assets/68dcef2a-eb1c-44fa-993b-acd6478a9760" />

# Race Condition in Multithreaded Algorithms

## 1. Definition
A **Race Condition** is a concurrency bug that occurs when two or more threads access shared data and try to change it at the same time. Because the thread scheduling algorithm can swap between threads at any time, the order in which the threads access the shared data is unknown (non-deterministic).

* **Core Issue:** The final outcome of the program depends on the relative timing ("race") of the threads.
* **Result:** Data corruption, inconsistent states, or "Lost Updates."

---

## 2. Technical Cause: The Critical Section
Race conditions happen when code execution involves a **Critical Section** that is not atomic.
A typical operation like `count++` actually consists of three CPU instructions:
1.  **LOAD:** Read value from memory to register.
2.  **ADD:** Increment value in register.
3.  **STORE:** Write register value back to memory.

If a context switch happens between step 1 and 3, the data becomes corrupted.

---

## 3. Example: The "Lost Update" Problem

Consider two threads, A and B, trying to increment a shared variable `Counter` (initially 5).

1.  **Thread A** reads `Counter` (Value: 5).
2.  *Context Switch occurs.*
3.  **Thread B** reads `Counter` (Value: 5).
4.  **Thread B** increments to 6 and writes it back.
5.  *Context Switch back to A.*
6.  **Thread A** (still thinking `Counter` is 5) increments to 6 and writes it back.

**Result:** The final value is 6.
**Expected:** The final value should be 7. (Thread B's update was "lost").

---

## 4. Visual Representation: Sequence of Events

The diagram below illustrates how interleaving causes the error.

```mermaid
sequenceDiagram
    participant T1 as "Thread 1"
    participant Mem as "Shared Memory (x=5)"
    participant T2 as "Thread 2"

    Note over T1, T2: Both want to increment x
    
    T1->>Mem: "1. READ x (Value 5)"
    activate T1
    
    T2->>Mem: "2. READ x (Value 5)"
    activate T2
    
    Note right of T2: T2 context runs
    T2-->>T2: "3. Increment (5 -> 6)"
    T2->>Mem: "4. WRITE x (Value 6)"
    deactivate T2
    
    Note left of T1: T1 resumes (Stale Data)
    T1-->>T1: "5. Increment (5 -> 6)"
    T1->>Mem: "6. WRITE x (Value 6)"
    deactivate T1
    
    Note over Mem: Final Result is 6 (Error!)
````

-----

## 5\. Prevention Mechanisms

To prevent race conditions, we must ensure **Mutual Exclusion** in the critical section. This is achieved using:

  * **Locks / Mutexes:** Only one thread can hold the lock at a time.
  * **Semaphores:** Signaling mechanism to control access.
  * **Atomic Variables:** Hardware-supported atomic operations (e.g., `AtomicInteger` in Java).

### Corrected Logic (Pseudocode)

```cpp
lock(mutex);       // Enter Critical Section
   x = x + 1;      // Safe Operation
unlock(mutex);     // Exit Critical Section
```

---

# Race Condition in Multithreaded Algorithms  
*(Clear, pointwise, technical keywords, small diagram — exam-ready)*

---

# 1. Definition

A **race condition** occurs in a multithreaded or parallel program when:

> Two or more threads **access a shared resource (variable, memory, file)** simultaneously, and the **final outcome depends on the timing or ordering** of their execution.

This leads to **unpredictable**, **inconsistent**, and **incorrect** results.

### **Technical Keywords:**  
shared resource, concurrent access, critical section, data inconsistency, unsynchronized threads, non-deterministic execution.

---

# 2. Why Race Conditions Occur

A race condition happens when all three conditions are met:

1. **Shared Data Exists**  
   Multiple threads access the same variable or memory location.

2. **At Least One Thread Writes**  
   Update or write operations occur concurrently.

3. **No Proper Synchronization**  
   Missing locks, mutexes, semaphores, or atomic operations.

---

# 3. Small Example (Conceptual)

Two threads increment a shared counter:

```text
Shared variable: X = 5

Thread 1: read X → 5
Thread 2: read X → 5
Thread 1: X = 5 + 1 = 6
Thread 2: X = 5 + 1 = 6   // should have been 7
````

Because both threads read the value **before either updated it**, the result is incorrect.

---

# 4. Small Diagram (Race Condition Timeline)

```text
Time →
Thread 1:   read X=5 ------ compute ------ write 6
Thread 2:        read X=5 ---------- compute ------ write 6

Correct result = 7
Actual result  = 6   ← Race condition
```

Outcome depends on scheduling → **non-deterministic**.

---

# 5. Consequences of Race Conditions

* Incorrect results
* Data corruption
* Program crashes or unpredictable behavior
* Hard-to-debug errors
* Violates safety in real-time or embedded systems

---

# 6. How to Prevent Race Conditions

(High-Level Brief)

* Use **mutual exclusion**: locks, mutexes
* Use **synchronization primitives**: semaphores, monitors
* Use **atomic operations**
* Protect shared data with a **critical section**

---

# 7. Exam-Ready Summary

* A **race condition** occurs when multiple threads **access and modify shared data without synchronization**, causing **non-deterministic** and **incorrect** outcomes.
* It arises due to unsynchronized concurrent writes.
* Prevented using **locks, semaphores, or atomic operations**.
* Crucial concept in **parallel programming**, **multithreading**, and **embedded systems**.

---


