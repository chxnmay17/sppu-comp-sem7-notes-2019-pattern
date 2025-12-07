<img width="524" height="101" alt="image" src="https://github.com/user-attachments/assets/820f9a5c-62e5-47e2-a382-9c203f3c5a69" />
5mks
# Distributed Minimum Spanning Tree (GHS Algorithm)

## 1. Algorithm Overview (GHS Algorithm)
The standard algorithm for finding a Minimum Spanning Tree (MST) in a distributed system is the **GHS Algorithm** (Gallager, Humblet, Spira).

**Goal:** In a weighted undirected graph where each node is a processor, construct a spanning tree with minimum total weight without a central controller.

### Key Technical Concepts
* **Fragment:** A connected subgraph of the MST. Initially, every node is a fragment of size 1.
* **MOE (Minimum Outgoing Edge):** The edge with the lowest weight connecting a node in a fragment to a node *outside* that fragment.
* **Levels:** Each fragment has a `Level`. Single nodes are Level 0.
* **Edge States:**
    * **Basic:** Undecided edge.
    * **Branch:** Part of the MST.
    * **Rejected:** Not part of the MST (leads to a node in the same fragment).

---

## 2. Algorithm Logic (Step-by-Step)

The algorithm proceeds in phases of **Finding** and **Merging**.

### Phase 1: Initialization (Level 0)
* Each node starts as an independent fragment.
* Each node wakes up and identifies its minimum weight incident edge.

### Phase 2: Finding the MOE
* The `Root` of a fragment broadcasts a message `Initiate` down the tree asking all nodes to find their best outgoing edge.
* Each node checks its neighbors:
    * If neighbor is in the **same** fragment $\to$ Edge is `Rejected`.
    * If neighbor is in a **different** fragment $\to$ Candidate for MOE.
* Leaves report their local minimum up to the root. The root selects the global MOE for the entire fragment.

### Phase 3: Merging Fragments
Fragments merge across their MOE.
1.  **Merge:** If Fragment A connects to Fragment B via edge $(u, v)$.
2.  **Level Update:**
    * If $Level(A) = Level(B)$, they merge into a new fragment of $Level + 1$. The edge $(u, v)$ becomes the new core.
    * If $Level(A) < Level(B)$, Fragment A is absorbed into B. Level remains $Level(B)$.

### Phase 4: Termination
* The process continues until only one fragment remains.
* This single fragment is the MST.

---

## 3. Visual Representation: Merging Fragments

The diagram below shows two fragments (Level 0) finding their Minimum Outgoing Edge and merging into a larger fragment (Level 1).

```mermaid
graph TD
    subgraph "Fragment 1 (Level 0)"
    A((Node A)) ---|"Branch"| B((Node B))
    end

    subgraph "Fragment 2 (Level 0)"
    C((Node C)) ---|"Branch"| D((Node D))
    end

    B -.-|"MOE (Weight 2)"| C
    A -.-|"Rejected (Weight 10)"| D

    style A fill:#e6f3ff,stroke:#333,color:#000
    style B fill:#e6f3ff,stroke:#333,color:#000
    style C fill:#ccffcc,stroke:#333,color:#000
    style D fill:#ccffcc,stroke:#333,color:#000
    
    linkStyle 2 stroke-width:4px,stroke:#00aa00;
````

-----

## 4\. Complexity Analysis

For a graph with $V$ nodes and $E$ edges:

1.  **Message Complexity:**

      * Each edge is rejected at most once.
      * Each level increase involves broadcasting messages.
      * Total Messages: **$O(E + V \log V)$**.

2.  **Time Complexity:**

      * Depends on the height of the fragments.
      * Total Time: **$O(V \log V)$** (in the worst case).

### Key Advantages

  * **Asynchronous:** Nodes do not need a global clock.
  * **Scalable:** Works efficiently for large-scale networks.

<!-- end list -->
---

# Distributed Minimum Spanning Tree (MST)  
*(Clear, pointwise, technical keywords, small diagram — exam-ready)*

---

# 1. Introduction

A **Minimum Spanning Tree (MST)** of a connected weighted graph is a tree that:

- Connects all the vertices  
- Has no cycles  
- Has **minimum total edge weight**

In **distributed systems**, the graph is spread across multiple processors/nodes.  
The classical MST algorithm for distributed environments is the **Gallager–Humblet–Spira (GHS) Algorithm**.

### **Technical Keywords:**  
distributed graph, message passing, local state, fragments, MOE (minimum outgoing edge), component merging, asynchronous communication.

---

# 2. Distributed MST: GHS Algorithm (High-Level Idea)

Each node initially behaves as its **own component**.  
Repeatedly:

1. Every component finds its **Minimum Outgoing Edge (MOE)**.  
2. Components **merge** using the MOE.  
3. Merging continues until there is **only one global MST component**.

This distributed approach avoids centralized control and works even with asynchronous communication.

---

# 3. GHS Distributed MST Algorithm (Stepwise Explanation)

### **Initialization**
- Each node considers itself as a **separate fragment**.
- Each node knows the weights of edges to its neighbors.
- Each fragment has:
  - A unique **fragment ID**
  - A **level** (height of the fragment tree)

---

## **Step 1: Find Minimum Outgoing Edge (MOE)**

Each fragment looks for the least-weight edge that connects it to a **different fragment**.

- Each node checks its adjacent edges.
- The minimum outgoing edge is reported to the fragment’s leader/root.

### Key Operation:
> **Each fragment independently identifies its lightest external edge.**

---

## **Step 2: Send Connect Message**

Once MOE is found:

- The fragment sends a **CONNECT** message along the MOE to the neighboring fragment.

Case 1: Neighbor fragment is at the **same level**  
→ Fragments merge and level increases.

Case 2: Neighbor fragment is at a **lower level**  
→ Lower-level fragment joins higher-level fragment.

Case 3: Neighbor fragment is at a **higher level**  
→ The connecting fragment waits until levels match.

---

## **Step 3: Merge Fragments**

After CONNECT message:

- The two fragments merge into a new, larger fragment.
- They assign:
  - New **fragment ID** (usually the ID of the MOE)
  - New **level** (either same or incremented)

Edges used in merging become part of the **MST**.

---

## **Step 4: Repeat Until Global MST is Formed**

Fragments continue repeating:

1. **Find MOE**  
2. **Send CONNECT**  
3. **Merge**

When all nodes belong to a **single fragment**, MST construction completes.

---

# 4. Small Diagram (Conceptual View of Fragment Merging)

```text
Initial fragments (each node is its own tree):

  A      B      C      D

Step 1: Find MOE and merge smallest edges:

  A──B       C──D

Step 2: Fragments find next MOE:

  A──B──────C──D

Step 3: Final MST after merging:

  A──B──────C──D
(One single fragment)
````

Nodes gradually merge into larger fragments using **minimum outgoing edges**.

---

# 5. Advantages of Distributed MST

1. **Scales to large distributed networks**

   * No central controller required.

2. **Fault-tolerant & asynchronous**

   * Works even when messages are delayed or processed independently.

3. **Minimizes communication overhead**

   * Nodes exchange only small messages (CONNECT, TEST, REPORT).

4. **Efficient for sparse networks**

   * Only relevant edges are tested.

---

# 6. Final Exam-Ready Summary

* Distributed MST is computed using the **GHS algorithm**, where nodes start as individual fragments.
* Each fragment repeatedly finds its **Minimum Outgoing Edge (MOE)**.
* Fragments merge using **CONNECT** messages.
* Fragment levels control merging order.
* Process repeats until all fragments integrate into a **single MST**.
* This approach is efficient, decentralized, and suitable for large distributed networks.

---


