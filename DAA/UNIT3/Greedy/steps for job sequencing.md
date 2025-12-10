The greedy approach used for the **Job Scheduling problem** (also known as job sequencing with deadlines) aims to schedule a subset of available jobs on a single processor to **maximize the total profit**.

The steps for applying the greedy approach to job scheduling are derived from the objective and the algorithm structure:

### 1. Sorting by Profit (Greedy Choice)
The first step is to **sort all jobs in decreasing order of profit**. This establishes the greedy choice property, ensuring that the algorithm considers the most profitable jobs first, making a locally optimal choice at each step.

### 2. Initialization
Initialize the set of scheduled jobs ($S$) to be empty ($\emptyset$) and the sum of the profit earned ($SP$) to zero.

### 3. Iterative Selection and Scheduling
The algorithm processes the jobs one by one from the sorted list and attempts to schedule them in a feasible time slot that meets the job's deadline. The scheduling algorithm is structured as follows:

*   **For each job $J[i]$** (starting from the most profitable):
    *   **Feasibility Check:** Check if scheduling the job $J[i]$ in a slot that satisfies its deadline constraint is feasible. A job $i$ must be completed by or before its deadline $d_i$, meaning if the job is scheduled in slot $t$, then $t \le d_i$.
    *   **Scheduling Decision (Irrevocable):** If the job is feasible, **schedule the job in the latest possible free slot meeting its deadline**.
    *   **Update:**
        *   Add the job to the set of scheduled jobs ($S$).
        *   Update the total earned profit ($SP$) by adding the job's profit $P[i]$.
    *   **Rejection:** If the job cannot be scheduled in a free slot that satisfies its deadline, **do not schedule the job** and move to the next item.

The process continues until all candidates are exhausted. The resulting set $S$ is a feasible schedule that maximizes the profit.
