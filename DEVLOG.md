# Development Log – The Torchbearer

**Student Name:** Marie-Jhayne Ayroso
**Student ID:** 827121627

---

## Entry 1 – [May 12th]: Initial Plan

For the initial plan I had planned on identifying which pieces of algorithms I wanted to use first and breaking it into small tasks. What I want to achieve first is to implement Dijkstra's algorithm to get the shortest-path distance before solving the relic problem. I think that the hardest part for me would be the recursive backtracking search since there is a possiblity of removing the optimal solutions. 

I plan on testing this by using Dijkstra's output on small graphs and then testing the entire pipeline

---

## Entry 2 – [May 13]: [Dijkstra Issue]

An issue I had was when I was implementing Dijkstra's algorithm. There were many incorrect paths that were being traced because some nodes were being processed multiple times. Since there were better distances, the priority queue had older entries even when a shorter path was already found to a node. I was able to resolve it by adding in the (if cost >dist[u]:continue). This was able to skip the processing when the current cost is grater than the stored distance.

---

## Entry 3 – [May 13]: [Recursive search and backtracking]

I had a problem when it came to implementing the recursive backtracking search. There was a problem with the remaining set of relics affecting other recursive branches which created some paths to skip relics that were necessary. I was able to fix this by removing and re-adding a relic before a recursive call. 

---

## Entry 4 – [May 13]: Post-Implementation Reflection

What I would change or improve if I had more time was the pruning strategy. Since pruning only uses the current best solution I would want a more efficient and easier solution to trace which can be done if I added a stronger lower-bound estimate. By doing this, I am able to stop recursive calls that are unnecessary.

---

## Final Entry – [May 13]: 10.70 Hours

| Part | Estimated Hours |
|---|---|
| Part 1: Problem Analysis | 1 |
| Part 2: Precomputation Design | 1.5 |
| Part 3: Algorithm Correctness | 0.40 |
| Part 4: Search Design | 0.30 |
| Part 5: State and Search Space | 2 |
| Part 6: Pruning | 2 |
| Part 7: Implementation | 2 |
| README and DEVLOG writing | 1.5 |
| **Total** | 10.70 |
