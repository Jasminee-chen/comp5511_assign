# comp5511 assignment1
# 2.STOCHASTIC DEMAND PROBLEM
## Project Overview

This project implements a genetic algorithm-based optimization solution for the Vehicle Routing Problem (VRP) with random demand. The approach accounts for real-world uncertainty in customer demand by incorporating an overload penalty mechanism into the fitness function, ensuring vehicle capacity constraints are met. The project aims to optimize routes to minimize total travel distance while accommodating demand variability.

## Problem Description

### Random Demand VRP Problem

According to the problem statement, the core issues addressed by this project are:
- Demand Uncertainty: Actual customer demand is a random variable following a normal distribution N(DEMAND, (0.2・DEMAND)²), where DEMAND is the mean value provided in VRP.csv, and demand values are truncated to positive integers.
- Constraints: Single vehicle, capacity limited to 200, must depart from and return to the warehouse.
- Operating Mode: Vehicles may make multiple trips to/from the warehouse (multiple deliveries) to fulfill all customer demands.
- Optimization Goal: Minimize the expected total travel distance under random demand.
- Comparative Analysis: Results must be compared with deterministic scenarios (Task 1), including metrics such as average distance and feasibility rate.

### Random Demand Model

In real-world VRPs, customer demand is often uncertain. This project employs the following model:
- The mean demand for each customer is the DEMAND value in VRP.csv
- Actual demand follows a normal distribution: N(DEMAND, (0.2·DEMAND)²)
- Demand values are truncated to positive integers (i.e., demand cannot be negative)

### Constraints

- Vehicle capacity constraint: 200
- Must start and return to the warehouse
- Must visit all customers
- Path must be feasible (does not exceed vehicle capacity)

## Installation Requirements

### Required Python Libraries

- Python 3.7+
- numpy
- pandas
- matplotlib
- deap

### Installation Commands

```bash
pip install numpy pandas matplotlib deap
```

## Usage

### Data Preparation

1. Prepare a CSV data file containing the following columns:
   - NO: Customer/Depot ID
   - CUST_OR_DEPOT: Indicates whether it's a customer (“CUST”) or depot (“DEPOT”)
   - XCOORD: X coordinate
   - YCOORD: Y coordinate
   - DEMAND: Average demand

2. Modify the data file path in the code:
   ```python
   file_path = “/Users/jasmine/Desktop/VRP.csv”  # Replace with your data file path
   ```

### Run Optimization

Directly execute the main program:

```bash
python stochastic_vrp.py
```

The program will perform the following steps:
1. Load and preprocess data
2. Run the genetic algorithm to optimize paths
3. Output optimal paths and total distance
4. Generate fitness evolution trend chart
5. Visualize optimal paths

## Algorithm Parameter Configuration

Adjust the following parameters in the configuration section of the code:

```python
VEHICLE_CAPACITY = 200    # Vehicle capacity
POP_SIZE = 100            # Population size
MAX_GEN = 150             # Maximum iterations
CXPB = 0.85               # Crossover probability
MUTPB = 0.2               # Mutation probability
RANDOM_SEED = 42          # Random seed
OVERLOAD_PENALTY = 10000  # Overload penalty
```

## Code Structure

### 1. Configuration and Data Loading

- Load CSV data file
- Separate depot and customer data
- Prepare location and demand data
- Compute distance matrix
- Create mapping from GA index to physical index

### 2. Route and Fitness Calculation

- `route_distance`: Calculate total route distance
- `evalVRP`: Evaluate individual fitness considering random demands and overload penalty

### 3. DEAP Framework Setup

- Create fitness function and individual types
- Register genetic algorithm operations (initialization, evaluation, crossover, mutation, selection)

### 4. Main Program Execution

- Run genetic algorithm
- Output optimal route and total distance
- Generate visualization charts

### 5. Visualization

- Plot fitness evolution trend chart
- Plot optimal path map

## Algorithm Principles

### Random Demand Handling

This project employs a deterministic equivalent approach to handle random demand:
- In the fitness function, approximate random demand using the mean demand plus a 20% safety margin
- This equates to assuming actual demand follows N(DEMAND, (0.2·DEMAND)²) at the 97.7th percentile
- Paths exceeding vehicle capacity incur significant penalty values

### Genetic Algorithm

The genetic algorithm optimizes customer visit sequences:
- **Individual Representation**: Permutations of customer visit sequences
- **Fitness Function**: Total path distance + Overload penalty
- **Selection**: Tournament selection
- **Crossover**: Ordered crossover
- **Mutation**: Index shuffling

## Result Interpretation

### Output Results

Output Results

After program execution, the following will be output:
- The minimum and average fitness values for each generation
- The expected total distance of the optimal path：3134.86


### Visualization Results

The program generates two visualizations:
1. **Fitness Evolution Plot**: Shows fitness changes during GA iterations
2. **Path Visualization**: Displays optimal paths and locations of customers/warehouses

### Comparison with Deterministic Scenarios

Under random demand conditions, compared to deterministic scenarios:
- **Average Distance**: Typically slightly longer due to accounting for demand uncertainty
- **Feasibility Rate**: Significantly improved as path design accommodates demand fluctuations
- **Robustness**: Paths exhibit greater resilience to demand variations

### Reference

https://github.com/DEAP/deap
