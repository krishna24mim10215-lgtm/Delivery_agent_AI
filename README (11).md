# CSA2001 - Autonomous Delivery Agent Project

This project, based on **CSA2001 - Fundamentals of AI and ML**, implements an autonomous agent that navigates a 2D grid city to deliver packages. The agent uses search algorithms to find efficient paths while considering static obstacles, variable terrain costs, and dynamic obstacles that require replanning.

## Features

- Models a **2D grid environment** where cells can represent paths, static obstacles, or terrain with different movement costs.
- Implements **Uniform-Cost Search (UCS)** to find the cheapest path based on terrain costs.
- Implements **A* Search** using the **Manhattan distance heuristic** to find a low-cost path efficiently.
- Includes **dynamic replanning**, allowing the agent to detect an unexpected obstacle and calculate a new route from its current position.
- Provides a **command-line interface (CLI)** for running simulations with different maps and algorithms.

## Project Structure

```text
.
├── autonomous_agent.py
├── map_generator.py
├── small_map.txt
├── medium_map.txt
├── large_map.txt
├── dynamic_map.txt
└── README.md
```

### File Description

| File | Description |
|---|---|
| `autonomous_agent.py` | Main Python script containing the environment, agent, search algorithms, and simulation logic. |
| `map_generator.py` | Python script for generating custom random maps. |
| `small_map.txt` | Small test map. |
| `medium_map.txt` | Medium test map. |
| `large_map.txt` | Large test map. |
| `dynamic_map.txt` | Map used for dynamic replanning simulations. |
| `README.md` | Project documentation. |

## Map File Format

The grid maps are represented as simple text files using the following symbols:

| Symbol | Meaning |
|---|---|
| `S` | Start position of the agent |
| `G` | Goal / delivery destination |
| `X` | Wall or static obstacle (impassable) |
| `.` or `1` | Standard terrain with movement cost `1` |
| `2-9` | Difficult terrain with the corresponding movement cost |
| `D` | Dynamic obstacle used for replanning simulations |

## Prerequisites

- Python **3.6 or higher**
- No external libraries are required.

## How to Run

### 1. Run a Specific Algorithm

Run an algorithm on a selected map using:

```bash
python autonomous_agent.py <map_file> <algorithm>
```

**Arguments:**

- `<map_file>` - Path to the map file, such as `small_map.txt`.
- `<algorithm>` - Search algorithm to use: `ucs` or `astar`.

**Example:**

```bash
python autonomous_agent.py medium_map.txt astar
```

The program will print:

- Path taken
- Total path cost
- Number of nodes expanded
- Execution time

### 2. Run the Dynamic Replanning Simulation

The dynamic simulation first plans a route and then introduces a dynamic obstacle during execution. The agent detects the obstacle and calculates a new route.

```bash
python autonomous_agent.py dynamic_map.txt dynamic
```

The output shows:

1. The initial plan
2. The point where the dynamic obstacle is detected
3. The newly calculated plan

### 3. Generate New Maps

Custom maps can be generated using `map_generator.py`:

```bash
python map_generator.py <width> <height> <output_filename> [--obstacles <num>]
```

**Example:**

```bash
python map_generator.py 30 20 my_map.txt --obstacles 50
```

This creates a **30 × 20** map named `my_map.txt` containing **50 random obstacles**. The generated file can then be edited to add the `S` (start) and `G` (goal) markers.

## Algorithms

### Uniform-Cost Search (UCS)

UCS finds the cheapest path by considering the movement cost of each terrain cell.

### A* Search

A* uses the **Manhattan distance heuristic** along with the path cost to efficiently search for a low-cost route.

### Dynamic Replanning

When a new obstacle appears on the planned route, the agent detects the change and recalculates its path from its current position.

## Notes

- Map files should contain valid `S` and `G` markers.
- `X` represents an impassable static obstacle.
- Terrain values from `2` to `9` represent increasing movement costs.
- The `D` marker is intended for dynamic replanning simulations.
