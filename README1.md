# comp5511 assignment1
# 1.Classical VRP

## Project Overview

This project implements a genetic algorithm-based optimization solution for the Single Vehicle Routing Problem (VRP). The solution aims to plan the optimal route for a single vehicle departing from a designated depot, servicing all customers, and returning to the depot while minimizing total travel distance under vehicle capacity constraints.

## Problem Description

According to the problem statement, this project addresses the following requirements:

1. **Constraints**:
   - Single vehicle with a capacity limit of 200
   - Must depart from and return to Depot No. 0
   - Route must satisfy vehicle capacity constraints (total demand ≤ 200)

2. **Optimization Objectives**:
   - Minimize total travel distance

3. **Data Sources**:
   - Customer locations (XCOORD, YCOORD) and demand (DEMAND) data from `VRP.csv` file

4. **Output Requirements**:
   - Visualize optimal route
   - Report total travel distance

## Installation Requirements

### Essential Python Libraries

- Python 3.7+
- pandas
- numpy
- matplotlib

### Installation Commands

```bash
pip install pandas numpy matplotlib
```

## Usage

### Data Preparation

1. Prepare a CSV data file containing the following columns:
   - CUST_OR_DEPOT: Identifies whether a location is a customer or a depot
   - XCOORD: X coordinate
   - YCOORD: Y coordinate
   - DEMAND: Demand
   - NO: ID (used to identify Depot 0)

2. Modify the data file path in the code:
   ```python
   file_path = “/Users/jasmine/Desktop/VRP.csv”  # Replace with your data file path
   ```

### Running the Optimization

Run the main program directly:

```bash
python vrp_single_vehicle.py
```

The program will perform the following steps:
1. Load and preprocess data
2. Run the genetic algorithm to optimize routes
3. Output the total distance of the optimal route
4. Generate a route visualization diagram
5. Generate an adaptation trend chart

## Algorithm Parameter Configuration

Adjust the following parameters in the configuration section of the code:

```python
POP_SIZE = 20        # Population size
MAX_GEN = 100        # Maximum iterations
MUT_RATE = 0.2       # Mutation probability
CROSS_RATE = 0.8     # Crossover probability
vehicle_capacity = 200  # Vehicle capacity
```

## Code Structure

### 1. Data Reading and Preprocessing

- Read CSV data file
- Separate warehouse and customer data
- Prepare location and demand data
- Determine starting warehouse index

### 2. Population Initialization

- `create_individual`: Generate a random customer visit sequence as an individual
- Create initial population

### 3. Fitness Function

- `fitness`: Calculate individual fitness values
  - Compute total route distance
  - Check capacity constraints, penalizing overloaded routes

### 4. Genetic Operators

- `tournament`: Tournament selection operator
- `crossover`: Ordered crossover (OX) operator
- `mutate`: Exchange mutation operator

### 5. Evolution Process

- Execute multiple generations of evolution
- Record optimal individuals
- Track fitness evolution

### 6. Result Visualization

- Plot optimal route map
- Plot fitness evolution trend chart

## Algorithm Principles

### Genetic Algorithm Overview

Genetic algorithms are optimization methods based on natural selection and genetics principles, simulating biological evolution to find optimal solutions. In this project, the genetic algorithm addresses the VRP problem through the following steps:

1. **Initialization**: Randomly generate a set of solutions (population)
2. **Evaluation**: Calculate the fitness (total route distance) for each solution
3. **Selection**: Choose superior individuals for reproduction based on fitness
4. **Crossover**: Generate new solutions through crossover operations
5. **Mutation**: Introduce random variations to enhance population diversity
6. **Iteration**: Repeat steps 2-5 until termination criteria are met

### Individual Representation

Each individual (chromosome) represents a customer visit sequence, expressed as a permutation of customer indices. For example, `[5, 12, 3, ..., 8]` denotes visiting customers with indices 5, 12, 3...8 in that order.

### Fitness Function

The fitness function calculates the total travel distance of a route and penalizes routes violating capacity constraints:

```python
def fitness(individual):
    total = 0  # Total distance
    load = 0   # Current load
    route = [depot0_index]  # Starting from depot 0
    for customer in individual:
        load += demands[customer]
        if load > vehicle_capacity:
            return 1e6  # Overload penalty
        total += np.linalg.norm(locations_all[route[-1]] - locations_all[customer])
        route.append(customer)
    total += np.linalg.norm(locations_all[route[-1]] - locations_all[depot0_index])
    return total
```

### Genetic Operators

1. **Selection**: Tournament Selection
   - Randomly select two individuals; retain the one with higher fitness

2. **Crossover**: Ordered Crossover (OX)
   - Select a segment of genes from Parent 1 to be directly inherited by the offspring
   - Fill the remaining genes sequentially from Parent 2, ensuring no repetition

3. **Mutation**: Swap Mutation
   - Randomly swap two customer positions to increase population diversity

## Result Interpretation

### Output Results

After running, the program will output:
1. Total distance of the optimal route：3644.1

### Visualization Results

The program generates two visual charts:

1. **Route Visualization Chart**:
   - Blue dots: Customer locations
   - Red squares: All warehouses (where warehouse 0 is the start/end point)
   - Black lines: Optimal driving route

2. **Fitness Evolution Trend Chart**:
   - Shows changes in optimal fitness (distance) during evolution
   - Reflects algorithm convergence

## Extension Suggestions

1. **Parameter Tuning**: Adjust genetic algorithm parameters (population size, iterations, crossover rate, mutation rate) to achieve better performance
2. **Alternative Evolutionary Algorithms**: Experiment with other evolutionary approaches like particle swarm optimization or ant colony optimization
3. **Local Search**: Integrate local search algorithms (e.g., 2-opt, 3-opt) for further path refinement
4. **Multi-Vehicle Extension**: Scale the model to handle multiple vehicles
5. **Time Window Constraints**: Incorporate time window constraints to solve VRP with time windows (VRPTW)
6. **Random Demand**: Account for uncertainty in customer demand
7. **Parallel Computing**: Accelerate solving large-scale problems using parallel computing

## Notes

1. Ensure the `VRP.csv` file path is correct; otherwise, a file-not-found error will occur
2. If total customer demand exceeds vehicle capacity (200), the algorithm returns a large penalty value. Check data or adjust capacity parameters
3. Algorithm results exhibit randomness; multiple runs may yield different optimal solutions
4. Solution quality can be improved by increasing population size and iteration count, but this increases computation time

## Reference
GA.m
