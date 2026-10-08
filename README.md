# SLE3
# Maze Solving System (BFS / DFS)

**SLE-3: Architectural Design (Full C4 Model)**
Course: 02AML204 – Introduction to Artificial Intelligence

| | |
|---|---|
| **Name** | Prasad Dinkar Gurav |
| **PRN** | 25UAM089 |
| **Division** | B |

---

## Overview

A search-based agent that finds a path through a grid maze from a start cell to an end cell. The maze (open cells and walls) is given as input, and the system explores it using either **Breadth First Search (BFS)** or **Depth First Search (DFS)**.

This is a core building block for robotics, games, and route-planning agents. The project continues directly from the BFS/DFS code and profiling work done in **SLE-1** and **SLE-2**.

## Features

- Solves grid mazes with walls, a start cell, and an end cell
- Two interchangeable algorithms: BFS (queue) and DFS (stack)
- Visited-set tracking to avoid revisiting cells and infinite loops
- Path reconstruction using parent links
- Reports "no path found" when the goal is unreachable
- Timing/profiling output from SLE-2
- Self-contained script with no network or API dependency

## Architecture (C4 Model)

| Level | View | Summary |
|---|---|---|
| 1 | **Context** | User gives a maze to the Maze Solver System and receives the path output |
| 2 | **Container** | Input module → Search engine → Output module, with a shared Visited set |
| 3 | **Component** | Search engine = Frontier → Explored set → Goal test → Path builder |
| 4 | **Code** | `generate_maze`, `bfs`, `dfs`, parent dictionary, path-reconstruction loop |

### Containers

- **Input module** – builds/loads the maze grid
- **Search engine** – runs BFS or DFS
- **Visited set** – stores explored cells
- **Output module** – shows the final path and profiling numbers

## Main Functions

| Function | Purpose |
|---|---|
| `generate_maze(size)` | Builds the maze grid used by both algorithms |
| `bfs(maze, start, end)` | Breadth First Search using a queue (FIFO) |
| `dfs(maze, start, end)` | Depth First Search using a stack (LIFO) |

## How It Works

1. The maze, start cell, and end cell are created or loaded.
2. The chosen algorithm pushes the start cell into the **frontier**.
3. Cells are popped, checked against the **goal test**, and marked in the **visited set**.
4. Each new cell's parent is recorded in a **parent dictionary**.
5. Once the goal is found, the path is rebuilt by walking parent links from end to start.

## Key Design Decision

BFS and DFS share almost identical logic. The **only structural difference is the frontier** (queue vs. stack). A single parent dictionary is reused for path reconstruction in both, instead of separate Node objects, which keeps the code simple and consistent.

## Usage

```bash
python maze_solver.py
```

> Replace `maze_solver.py` with your actual script name.

## Related Work

- **SLE-1** – BFS/DFS implementation
- **SLE-2** – Profiling and performance comparison
- **SLE-3** – Architectural design (this project)

## AI Contribution

See [`AI_CONTRIBUTION_LOG.md`](AI_CONTRIBUTION_LOG.md).
