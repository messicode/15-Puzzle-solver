# 15‑Puzzle Solver — A* Manhattan Heuristic & IDDFS Search

## Features
* **A\* with Manhattan‑distance heuristic** – finds optimal solution depths ≤ 80 in ≤ 0.1 s on consumer laptops.  
* **Iterative Deepening DFS (IDDFS)** – memory‑frugal alternative for very deep scrambles.  
* **State canonicalisation & duplicate detection** using `unordered_set` hash keys.  
* **Metrics** – prints expanded nodes, elapsed time, and approximate memory footprint.  
* **CLI & stdin modes** – `./solver 1 2 3 … 0` or piped board input.  
* **Unit tests** – GoogleTest cases for solvable/unsolvable positions and heuristic admissibility.

## Solvabilty of puzzle
There is a method to check whether any given game state is solvable.
```
   1. If the grid width is odd, then the number of inversions in a solvable situation is even.
   2. If the grid width is even, and the blank is on an even row counting from the bottom (second-last, fourth-last etc), then the number of inversions in a solvable situation is odd.
   3. If the grid width is even, and the blank is on an odd row counting from the bottom (last, third-last, fifth-last etc) then the number of inversions in a solvable situation is even.
```
While , An inversion is when a tile precedes another tile with a lower number on it. The solution state has zero inversions. for more information see

## Iterative Deepening Depth First Search Algorithm
DFS in a BFS fashion
Iterative deepening depth-first search (IDDFS) is an extension to the ‘vanilla’ depth-first search algorithm, with an added constraint on the total depth explored per iteration. This addition produces equivalent results to what can be achieved using breadth-first search, without suffering from the large memory costs. Due to BFS’s storage of fringe vertices in memory, Od^b memory space may be required (b = branching factor), this is a stark contrast to IDDFS’s O(bd) worst-case memory requirements.

## A-star searching Algorithm with Manhattan Heuristic
A-star is an informed (heuristic) search algorithm, meaning that it solves problems (pathfinding) by searching among all possible paths to the solution (goal) for the one that incurs the smallest cost (manhattan distance here), and among these paths it first considers the ones that appear to lead most quickly to the solution. At each iteration of its main loop, A-star needs to determine which of its partial paths to expand into one or more longer paths. It does so based on an estimate of the cost (total weight) still to go to the goal node. Specifically, A-star selects the path that minimizes 
```
f(n)=g(n)+h(n)
```
where n is the last node on the path, g(n) is the cost of the path from the start node to n, and h(n) is a heuristic that estimates the cost of the cheapest path from n to the goal.


## Build & Run
Run using mingw32
```
cd path\to\your\file
g++ yourfile.cpp -o yourprogram
./yourprogram
```

**Why AD/ADAS relevance?**  
Path–search for a sliding‑tile puzzle maps to motion‑planning in autonomous driving:  
each board configuration is a vehicle “state”, a move is a low‑level control action,  
and the heuristic guides the planner to the goal with minimal search effort.


## AD/ADAS Analogy
| Puzzle                             | Autonomous System                |
|------------------------------------|----------------------------------|
| Board state                        | Vehicle pose + environment state |
| Move (tile slide)                  | Low‑level maneuver (lane shift)  |
| Manhattan heuristic                | Cost‑to‑go estimate (drivable‑space distance) |
| Closed/Visited set                 | Collision‑check cache            |
| Optimal path                       | Feasible, minimum‑cost trajectory |


