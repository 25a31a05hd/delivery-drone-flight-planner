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
