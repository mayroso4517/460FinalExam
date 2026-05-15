# The Torchbearer

**Student Name:** Marie-Jhayne Ayroso
**Student ID:** 827121627
**Course:** CS 460 – Algorithms | Spring 2026

> This README is your project documentation. Write it the way a developer would document
> their design decisions , bullet points, brief justifications, and concrete examples where
> required. You are not writing an essay. You are explaining what you built and why you built
> it that way. Delete all blockquotes like this one before submitting.

---

## Part 1: Problem Analysis

> Document why this problem is not just a shortest-path problem. Three bullet points, one
> per question. Each bullet should be 1-2 sentences max.

- **Why a single shortest-path run from S is not enough:**
  A single shortest-path run from S is not enough because it will only look for the cheapest path starting from S and going to each node. We must go through all the paths to find the most efficient sequence that will collect all the relics and reach the end. 

- **What decision remains after all inter-location costs are known:**
 Once all the shortest-path distances are found, the algorithm will find the most efficient order of visiting all relics before reaching the end.

- **Why this requires a search over orders (one sentence):**
 It requires a search over because searching each relic can lead to different options which is why the algorithm finds the cheapest route by searching through all the possible outcomes. 

---

## Part 2: Precomputation Design

### Part 2a: Source Selection

> List the source node types as a bullet list. For each, one-line reason.

| Source Node Type | Why it is a source |
|---|---|
| Start node (S) | Starting position to compute shortest path to every relic and to the exit node |
| Relic nodes (R1, R2, ..., Rk) | Since each relic must be visited, we compute the shortest path from each one to all other important nodes|
| Exit node (T) | Exit position from all other nodes which is used for the shortest path.|

### Part 2b: Distance Storage

> Fill in the table. No prose required.

| Property | Your answer |
|---|---|
| Data structure name | Nested dictionary |
| What the keys represent | Outer key = starting node, Inner key: destination node|
| What the values represent | The minimum shortest-path distance between the starting and destination node|
| Lookup time complexity | O(1) |
| Why O(1) lookup is possible | Hashing allows O(1) to access the values without searching through all the entries |

### Part 2c: Precomputation Complexity

> State the total complexity and show the arithmetic. Two to three lines max.

- **Number of Dijkstra runs:** O(k)
- **Cost per run:** O(m log n)
- **Total complexity:** O(k · m log n)
- **Justification (one line):** For each source node, we are using Dijkstra which uses a priority queue to find the shortest path algoirthm

---

## Part 3: Algorithm Correctness

> Document your understanding of why Dijkstra produces correct distances.
> Bullet points and short sentences throughout. No paragraphs.

### Part 3a: What the Invariant Means

> Two bullets: one for finalized nodes, one for non-finalized nodes.
> Do not copy the invariant text from the spec.

- **For nodes already finalized (in S):**
  Nodes already finalized show that it has a distance with the most optimal cost from the starting node which means that there is no other shortest path found later.

- **For nodes not yet finalized (not in S):**
 Nodes not yet finalized only have the best known distance that is stored so far but can be changed if there is another shortest path found.

### Part 3b: Why Each Phase Holds

> One to two bullets per phase. Maintenance must mention nonnegative edge weights.

- **Initialization : why the invariant holds before iteration 1:**
  Since it starts at the node with a distance of 0 and all other nodes are infinity, no path has been searched which shows that the invariant holds.

- **Maintenance : why finalizing the min-dist node is always correct:**
  All edge weights are nonnegative meaning that any other path that is connected to that node cannot produce a smaller distance which shows that it is already optimal when finalized.

- **Termination : what the invariant guarantees when the algorithm ends:**
  Guarantees that all reachable nodes contained its optimal shortest-path distance from the starting point.

### Part 3c: Why This Matters for the Route Planner

> One sentence connecting correct distances to correct routing decisions.

Correct routing decisions depend on correct shortest-path distances to determine the optimal order of visiting relics with minimum total cost.

---

## Part 4: Search Design

### Why Greedy Fails

> State the failure mode. Then give a concrete counter-example using specific node names
> or costs (you may use the illustration example from the spec). Three to five bullets.

- **The failure mode:** Greedy fails because it chooses the closest next node without considering the other sequences of relic vists that can lead to a more optimal solution
- **Counter-example setup:** Start at S, path to R1 is cheaper and connects directly to the exit and R2 allows a shorter overall route to the exit.
- **What greedy picks:** Greedy chooses the closest available relic first since it is locally optimal
- **What optimal picks:** Optimal chooses a different path with the lowest total cost from the starting node to the target node 
- **Why greedy loses:** Since greedy stays ahead by choosing the locally optimal solution, it can miss better overall paths that use a different route 

### What the Algorithm Must Explore

> One bullet. Must use the word "order."

- Algorithm must explore all the possible orders of visiting the relic that will find the lowest-cost route.

---

## Part 5: State and Search Space

### Part 5a: State Representation

> Document the three components of your search state as a table.
> Variable names here must match exactly what you use in torchbearer.py.

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | current_loc | node | Tracks node of current position during the search |
| Relics already collected | relics_remaining | set | Stores relics that need to be collected |
| Fuel cost so far | cost_so_far | float | Total fuel of start node to current |

### Part 5b: Data Structure for Visited Relics

> Fill in the table.

| Property | Your answer |
|---|---|
| Data structure chosen | Set |
| Operation: check if relic already collected | Time complexity: O(1) |
| Operation: mark a relic as collected | Time complexity: O(1) |
| Operation: unmark a relic (backtrack) | Time complexity: O(1) |
| Why this structure fits | Allows efficient membership checking as well as add and remove for backtracking|

### Part 5c: Worst-Case Search Space

> Two bullets.

- **Worst-case number of orders considered:** O(k!)
- **Why:** Every order of the k relics must be tried in order to find the minimum-cost route 

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

> Three bullets.

- **What is tracked:** Current route with the lowest total fuel cost
- **When it is used:** When a new valid route is found through recursive exploration
- **What it allows the algorithm to skip:** Incomplete routes with a higher current cost than the best known 

### Part 6b: Lower Bound Estimation

> Three bullets.

- **What information is available at the current state:** Current location, current cost, and remaining relics to visit
- **What the lower bound accounts for:** Current path cost and estimate of the remaining cost to reach the end
- **Why it never overestimates:** Shortest-path represents the minimum travel costs which shows that the estimate will not overestimate.

### Part 6c: Pruning Correctness

> One to two bullets. Explain why pruning is safe.

- It is safe because any path whose current cost already exceeds the best known solution cannot be improved into a better complete route.
- Extending a path will only increase or maintain the current cost because all edge weights are nonnegative.

---

## References

> Bullet list. If none beyond lecture notes, write that.

- _Your references here._
