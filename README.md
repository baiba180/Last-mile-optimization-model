# Autonomous Vehicle Dispatching and Ride-Pooling Simulations

This repository provides four event-based simulation models for hub-based autonomous vehicle operations:

1. **Single-Passenger Dispatching**  
   Real-time assignment of dedicated vehicles to individual passenger requests.

2. **2-Passenger Real-time Ride-Pooling**  
   Dynamic on-the-fly pairwise matching with a strict 293-second maximum waiting time constraint.

3. **Pre-matched Two-Passenger Ride-Sharing**  
   Batch optimization using exact set-partitioning formulation (batch sizes 4, 6, 8, 10) solved by Gurobi, followed by real-time vehicle dispatching.

4. **2-passenger Real-time Ride-Pooling Simulation with En-route transfer module**  
   The en-route transfer module solved by Gurobi has been integrated into the 2-passenger code, allowing adjustment of minimum transfer limits, time windows, and maximum number of vehicles.

All models enforce:
- Maximum passenger waiting time of 293 seconds at the hub
- Vehicle capacity of 2 passengers
- Radial routing strategy (destinations served in increasing distance order from hub)
- Precomputed shortest-path distances using Dijkstra on sparse CSR network representation
- System cost = passenger total time + loaded distance + empty return distance + vehicle cost at hub

## Input Data (place in `data/` folder)

- `node_id.csv` – Node ID to index mapping
- `csr_mat.npz` – Road network adjacency matrix in SciPy CSR format
- `demand.csv` – Passenger requests with columns:
  - `pickup_time` (Time when the request was submitted, seconds from simulation start)
  - `dropoff_node` (destination node ID)

## Output

Each script saves results in the `results/` directory:
- Performance comparison across fleet sizes and batch configurations
- Detailed records of en-route transfer opportunities (Module 4) when enabled

## Requirements

```bash
pip install pandas numpy scipy matplotlib seaborn gurobipy
If your Python version is lower than 3.7: pip install dataclasses

## Citation
Please cite the following paper if you use this code in your research:
Bao, H., Luo, X., Su, Q., & Wang, H. (2025). Optimizing last-mile public transit services by leveraging modular autonomous vehicles. Journal of Transportation Engineering, Part A: Systems, 151(8). https://doi.org/10.1061/JTEPBS.TEENG-8954
