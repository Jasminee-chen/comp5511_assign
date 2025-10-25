# comp5511_assign
## Pickup and Delivery Problem Solution

## Project Overview

This project implements an evolutionary algorithm-based solution for the Pickup and Delivery Problem (PDP). This problem is a variant of the Vehicle Routing Problem (VRP), where some customers require deliveries (positive demand) while others require pickups (negative demand). The vehicle's net load must always remain within the range [0, 200].

## Problem Description

- Input data includes a distribution center and multiple customer locations
- 30% of customers are randomly selected as pickup points (negative demand)
- The remaining 70% of customers serve as delivery points (positive demand)
- Vehicles must depart from the distribution center, serve all customers, and return to the distribution center
- The vehicle's net load must always remain within the range [0, 200]
- The objective is to minimize total travel distance while satisfying all constraints

## Solution

### Algorithm Design

This project employs an Evolutionary Algorithm to solve the problem:

1. **Individual Representation**: Each individual represents a complete delivery plan comprising multiple paths
2. **Fitness Function**: Simultaneously considers total distance and constraint violation severity
3. **Selection Operator**: Tournament selection
4. **Crossover Operator**: Partial Mapping Crossover (PMX)
5. **Mutation Operator**: Swap mutation, incorporating path count variation

### Key Features

1. **Data Loading & Preprocessing**: Load data from CSV files, randomly assign pickup and delivery points
2. **Distance Calculation**: Computes Euclidean distances between nodes
3. **Evolutionary Algorithm Settings**: Configures algorithm parameters and operators
4. **Algorithm Execution**: Runs evolutionary algorithm to find optimal solutions
5. **Result Visualization**: Plots optimal paths and evolutionary process
6. **Result Analysis**: Analyzes path feasibility and load conditions

## Usage Instructions

### Environment Requirements

- Python 3.x
- pandas
- numpy
- matplotlib
- deap

### Install Dependencies

```bash
pip install pandas numpy matplotlib deap
```

### Data Format

Input data file (VRP.csv) should contain the following columns:
- NO: Node ID
- CUST_OR_DEPOT: Node type (‘CUSTOMER’ or ‘DEPOT’)
- XCOORD: X coordinate
- YCOORD: Y coordinate
- DEMAND: Demand quantity

### Running the Program

```python
if __name__ == “__main__”:
    # Load data
    file_path = ‘/path/to/your/VRP.csv’
    nodes, depots, customers = load_data(file_path)

    # Set up evolutionary algorithm
    toolbox = setup_ea(customers, depots)

    # Run evolutionary algorithm
    best_ind, log = run_ea(toolbox, pop_size=100, generations=50)

    # Visualize optimal routes
    routes = visualize_routes(best_ind, nodes, depots, “Optimal Route of VRP with Pickup and Delivery”)

    # Analyze results
    analyze_results(best_ind, nodes, depots)

    # Plot evolutionary curve
    gen = log.select(“gen”)
    avg_dist = [log.select(“avg”)[i][0] for i in range(len(log))]
    min_dist = [log.select(“min”)[i][0] for i in range(len(log))]

    plt.figure(figsize=(10, 6))
    plt.plot(gen, avg_dist, label="average distance")
    plt.plot(gen, min_dist, label="minimum distance")
    plt.xlabel(‘Generation’)
    plt.ylabel(‘Distance’)
    plt.title(‘Evolution of Distance’)
    plt.legend()
    plt.grid(True)
    plt.show ()
```

## Result Interpretation

### Visual Output

1. **Path Map**:
   - Red squares: Distribution centers
   - Blue circles: Delivery points (positive demand)
   - Green triangles: Pickup points (negative demand)
   - Lines of different colors: Different delivery paths

2. **Evolutionary Curve Chart**:
   - Blue line: Average distance
   - Green line: Minimum distance
   - X-axis: Evolutionary generation
   - Y-axis: Distance

### Console Output

- Total distance: Total travel distance of the optimal solution
- Details for each path:
  - Node sequence
  - Maximum load
  - Minimum load
- Constraint satisfaction: Whether all paths meet the load constraint [0, 200]

## Algorithm Parameters

Adjust the following parameters as needed:

- `pop_size`: Population size, default 100
- `generations`: Number of evolutionary generations, default 50
- `cxpb`: Crossover probability, default 0.7
- `mutpb`: Mutation probability, default 0.2
- `max_load`: Maximum vehicle load, default 200

