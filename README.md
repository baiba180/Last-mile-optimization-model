# Autonomous Vehicle Dispatching and Ride-Pooling Simulations

This repository provides four event-based simulation models for hub-based autonomous vehicle operations:

1. **Single-Passenger Dispatching**  
   Real-time assignment of dedicated vehicles to individual passenger requests.

2. **2-Passenger Real-time Ride-Pooling**  
   Dynamic on-the-fly pairwise matching with a strict 293-second maximum waiting time constraint.

3. **Pre-matched Two-Passenger Ride-Sharing**  
   Batch optimization using exact set-partitioning formulation (batch sizes 4, 6, 8, 10) solved by Gurobi, followed by real-time vehicle dispatching.

4. **En-route Passenger Transfer (Offline Trajectory Re-optimization)**  
   Post-simulation module that identifies spatial-temporal crossings between completed vehicle trajectories and reassigns passengers across trips to reduce total vehicle operating time. Supports configurable time window (e.g., 5 seconds) for crossing detection.

All models enforce:
- Maximum passenger waiting time of 293 seconds at the hub
- Vehicle capacity of 2 passengers
- Radial routing strategy (destinations served in increasing distance order from hub)
- Precomputed shortest-path distances using Dijkstra on sparse CSR network representation
- System cost = passenger total time + loaded distance + empty return distance + vehicle idle time at hub

## Input Data (place in `data/` folder)

- `node.csv` – Node ID to index mapping
- `csr_mat.npz` – Road network adjacency matrix in SciPy CSR format
- `demand.csv` – Passenger requests with columns:
  - `pickup_time` (seconds from simulation start)
  - `dropoff_node` (destination node ID)

## Output

Each script saves results in the `results/` directory:
- Performance comparison across fleet sizes and batch configurations
- Detailed records of en-route transfer opportunities (Module 4) when enabled

## Requirements

```bash
pip install pandas numpy scipy gurobipy

## Citation
Please cite the following paper if you use this code in your research:
APA (7th Edition)
Bao, H., Luo, X., Su, Q., & Wang, H. (2025). Optimizing last-mile public transit services by leveraging modular autonomous vehicles. Journal of Transportation Engineering, Part A: Systems, 151(8). https://doi.org/10.1061/JTEPBS.TEENG-8954
