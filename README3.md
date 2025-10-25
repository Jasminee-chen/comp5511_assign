# comp5511 assignment1
# LARGE-SCALE OPTIMIZATION PROBLEM
## Project Overview

This project implements a large-scale Vehicle Routing Problem (VRP) optimization solution based on clustering and genetic algorithms. The approach groups customer locations using K-means clustering and employs genetic algorithms to optimize routes, solving a VRP problem involving 200 customer locations. Vehicles must visit all customers within a single area before moving to another.

## Problem Description

### Large-Scale VRP Problem

Requirements:
1. Create 100 additional customers by shifting each customer's Y-coordinate in VRP.csv by 150
2. Form a large-scale VRP problem with 200 customers (retaining the original depot point, numbered 0)
3. Group customers into distinct regions using clustering algorithms (e.g., K-means or DBSCAN)
4. Vehicles must visit all customers within one region before moving to another
5. Develop an evolutionary algorithm incorporating clustering to solve this large-scale VRP
6. Visualize clustered routes and report total distance

### Objective Function

Minimize the total distance traveled by vehicles while satisfying these constraints:
- Vehicles depart from the depot, visit all customer points, and return to the depot
- Vehicles must visit all customers within one zone before moving to another zone

## Installation Requirements

### Required Python Libraries

- Python 3.7+
- numpy
- pandas
- matplotlib
- scikit-learn
- deap

### Installation Commands

```bash
pip install numpy pandas matplotlib scikit-learn deap
```

## Usage

### Data Preparation

1. Prepare a CSV data file containing the following columns:
   - NO: Customer/Depot ID
   - CUST_OR_DEPOT: Indicates whether it's a customer (“CUST”) or depot (“DEPOT”)
   - XCOORD: X coordinate
   - YCOORD: Y coordinate
   - DEMAND: Demand

2. Modify the data file path in the code:
   ```python
   file_path = “/Users/jasmine/Desktop/VRP.csv”  # Replace with your data file path
   ```

### Run Optimization

Directly run the main program:

```bash
python large_scale_vrp.py
```

The program will perform the following steps:
1. Load data and create an additional 100 customer points
2. Cluster customer points using the K-means algorithm
3. Run the genetic algorithm to optimize routes
4. Output the total distance for each individual
5. Visualize optimal routes and clustering results
6. Plot the fitness evolution trend chart

## Algorithm Parameter Configuration

The following parameters can be adjusted in the configuration section of the code:

```python
VEHICLE_CAPACITY = 200  # Capacity negligible for single-vehicle runs
K_CLUSTERS = 5          # Number of clusters
POP_SIZE = 100          # Population size
MAX_GEN = 250           # Maximum iterations
CX_PB = 0.85            # Crossover probability
MUT_PB = 0.3            # Mutation probability
```

## Code Structure

### 1. Configuration and Data Loading

- Load CSV data file
- Create 100 additional customer points (Y-coordinate shifted by 150)
- Prepare location and demand data
- Compute distance matrix

### 2. Clustering

- Cluster customer points using K-means algorithm
- Assign customer indices to each cluster

### 3. DEAP Framework Setup

- Create fitness function and individual types
- Define individual initialization function (includes clustering order and internal order)
- Register genetic algorithm operations

### 4. Path Conversion and Fitness Calculation

- `individual_to_route`: Convert genetic algorithm individuals to actual routes
- `route_distance`: Calculate total route distance
- `eval_vrp`: Evaluate individual fitness

### 5. Genetic Operators

- `cx_vrp`: Crossover operator, simultaneously crosses cluster order and internal order
- `mut_vrp`: Mutation operator, randomly shuffles cluster order and internal order

### 6. Running the Genetic Algorithm

- `run_ga`: Executes the genetic algorithm and returns the optimal individual

### 7. Main Program

- Executes the optimization process
- Outputs results
- Generate visualization charts

### 8. Visualization

- Plot optimal paths and clustering results
- Plot fitness evolution trend chart

## Algorithm Principles

### Clustering Phase

Use the K-means algorithm to cluster 200 customer points into K regions. The K-means algorithm operates through the following steps:
1. Randomly select K center points
2. Assign each customer point to the nearest center point
3. Update center points as the average of each cluster
4. Repeat steps 2 and 3 until convergence

### Genetic Algorithm Phase

The genetic algorithm optimizes two levels of order:
1. **Cluster Order**: Sequence for vehicle visits to different cluster regions
2. **Internal order**: The sequence of customer visits within each clustered area

Genetic algorithm operations:
- **Selection**: Tournament selection
- **Crossover**: Ordered crossover (for clustering order) and two-point crossover (for internal order)
- **Mutation**: Index shuffling (for both clustering and internal orders)

## Result Interpretation

### Output Results

After running, the program outputs:
1. Average fitness and minimum fitness for each generation
2. Total distance of the optimal path
3. Total distance for each individual

### Visualization Results

The program generates two visual charts:
1. **Cluster Path Map**: Displays clustering results of customer points and the optimal path
2. **Fitness Evolution Plot**: Shows fitness changes during the genetic algorithm's iterations

### Cluster Path Map Notes

- Different colored points represent distinct cluster regions
- Red squares denote warehouses
- Black lines indicate vehicle travel paths
- Vehicles must visit all customers within a region before moving to another
