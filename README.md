## Delivery Drone Flight Planner

A smart, interactive route-planning system for autonomous drone deliveries.  
This project helps users design efficient flight paths across a grid-based environment while avoiding restricted zones, minimizing travel distance, and estimating energy consumption.

---

# 🌍 Project Overview

The Delivery Drone Flight Planner is a web-based application that allows users to:

- place a drone base station
- add delivery target points
- mark no-fly zones and blocked cells
- compute shortest safe routes using BFS
- optimize the full route using TSP-based algorithms
- visualize the final path on a grid
- estimate distance, flight time, and battery usage
- animate the drone movement along the computed route

This project demonstrates how autonomous drone systems can make smart delivery decisions in real-world logistics scenarios.

---

# ✨ Key Features

- Interactive grid map editor
- Base station and delivery point placement
- Obstacle / no-fly zone drawing
- Shortest path computation using BFS
- Pairwise route cost matrix generation
- Exact optimization using Held-Karp algorithm
- Fast heuristic optimization using Greedy Nearest Neighbor
- Live mission metrics
- Battery and energy estimation
- Animated drone route simulation
- Preset scenarios for different map layouts
- Simple browser-based user interface

---

# 🧠 How It Works

The system follows a structured workflow:

1. Initialize the grid environment and drone settings
2. Add base location and delivery points
3. Define restricted no-fly zones
4. Compute shortest valid paths between all points
5. Build a cost matrix for route planning
6. Select the optimization strategy
7. Generate the final delivery route
8. Render and animate the drone path
9. Display mission metrics and battery status

---

# 🏗️ Architecture

```mermaid
flowchart TD
    A([Start / Application Launch]) --> B[Initialize Grid Environment & Drone Parameters]

    B --> C{User Input Action}

    C -->|Set Locations| D[Place Base Station & Delivery Points]
    C -->|Set Obstacles| E[Draw / Toggle No-Fly Zones]
    C -->|Select Preset| F[Load Sample Map Scenario]

    D --> G[Generate Adjacency Graph]
    E --> G
    F --> G

    G --> H[Run Breadth-First Search - BFS]

    H --> I{Clear Path Found Between All Locations?}

    I -->|No| J[Display Error: 'Delivery location unreachable due to No-Fly Zone']
    J --> C

    I -->|Yes| K[Construct All-Pairs Shortest Path Matrix & Energy Costs]

    K --> L{Select TSP Optimization Method}

    L -->|Small Point Count <= 12| M[Run Dynamic Programming Algorithm - Held-Karp]
    L -->|Large Point Count > 12| N[Run Greedy Heuristic - Nearest Neighbor]

    M --> O[Compute Exact Optimal Path & Minimal Battery Usage]
    N --> O[Compute Near-Optimal Path & Estimated Battery Usage]

    O --> P[Render Drone Flight Path on Grid]
    P --> Q[Animate Flight Trajectory & Display Performance Metrics]

    Q --> R([End / Await Next Input])
flowchart TD
    A([Start / Application Launch]) --> B[Initialize Grid Environment & Drone Parameters]
    
    B --> C{User Input Action}
    
    C -->|Set Locations| D[Place Base Station & Delivery Points]
    C -->|Set Obstacles| E[Draw / Toggle No-Fly Zones]
    C -->|Select Preset| F[Load Sample Map Scenario]
    
    D --> G[Generate Adjacency Graph]
    E --> G
    F --> G
    
    G --> H[Run Breadth-First Search - BFS]
    
    H --> I{Clear Path Found Between All Locations?}
    
    I -->|No| J[Display Error: 'Delivery location unreachable due to No-Fly Zone']
    J --> C
    
    I -->|Yes| K[Construct All-Pairs Shortest Path Matrix & Energy Costs]
    
    K --> L{Select TSP Optimization Method}
    
    L -->|Small Point Count <= 12| M[Run Dynamic Programming Algorithm - Held-Karp]
    L -->|Large Point Count > 12| N[Run Greedy Heuristic - Nearest Neighbor]
    
    M --> O[Compute Exact Optimal Path & Minimal Battery Usage]
    N --> O[Compute Near-Optimal Path & Estimated Battery Usage]
    
    O --> P[Render Drone Flight Path on Grid]
    P --> Q[Animate Flight Trajectory & Display Performance Metrics]
    
    Q --> R([End / Await Next Input])
    +-----------------------------------------------------------------------+
|                         1. INITIALIZATION                             |
|  - Load grid dimensions, battery capacity, and default coordinates.   |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|                      2. USER / PRESET INPUTS                          |
|  - Define Base Location (Start/End Node)                              |
|  - Define Delivery Destinations                                       |
|  - Plot No-Fly Zones (Blocked Grid Cells)                             |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|                    3. PATHFINDING LAYER (BFS)                         |
|  - Calculate shortest obstacle-avoiding paths between all pairs.      |
|  - If any point is unreachable -> Prompt user to adjust no-fly zones. |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|                   4. COST MATRIX CONSTRUCTION                         |
|  - Distance = Number of grid step traversals via BFS.                 |
|  - Energy Cost = Distance * Energy Consumption Rate per step.          |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|                     5. TSP ROUTE OPTIMIZATION                         |
|                                                                       |
|   [N <= 12 Points]                          [N > 12 Points]           |
|   ---> Held-Karp DP (Bitmask)               ---> Greedy Heuristic     |
|   * Guarantees exact minimum path           * Rapid computation       |
|   * Complexity: O(n² · 2ⁿ)                  * Complexity: O(n²)     |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|                 6. VISUALIZATION & METRICS DISPLAY                    |
|  - Draw line paths connecting points through clear coordinates.       |
|  - Animate drone marker traveling along flight path.                  |
|  - Output summary: Total Distance, Energy Used, Remaining Battery.   |
+-----------------------------------------------------------------------+




## Project Architecture Flowchart

```mermaid
<paste the mermaid code here>
```
