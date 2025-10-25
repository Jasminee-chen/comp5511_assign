# comp5511 assignment1
# 4.MULTI-OBJECTIVE OPTIMIZATION PROBLEM

## Project Overview

This project implements a multi-objective Vehicle Routing Problem (VRP) optimization solution based on genetic algorithms. The solution employs two distinct optimization strategies to address the VRP: a weighted single-objective genetic algorithm and the NSGA-II multi-objective optimization algorithm. The goal is to simultaneously minimize total travel distance and maximize overall efficiency, delivering optimal solutions for logistics distribution and route planning.
## Problem Description

The Vehicle Routing Problem (VRP) is a classic combinatorial optimization problem. Its objective is to find an optimal set of routes enabling vehicles to visit all customer locations and return to the starting point at minimal cost (typically distance or time). This project considers two optimization objectives:

1. **Minimize Total Travel Distance** (f₁): The total distance traveled by a vehicle from the depot, visiting all customer locations, and returning to the depot.
2. **Maximize total efficiency** (f₂): Calculate total efficiency by considering each customer point's efficiency value and the cumulative distance to reach that point.

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
   - XCOORD: X-coordinate of customer points
   - YCOORD: Y-coordinate of customer points
   - DEMAND: Customer demand (demand for the warehouse should be 0)
   - EFFICIENCY: Efficiency value of the customer point

2. Modify the data file path in the code:
   ```python
   DATA_FILE = ‘/Users/jasmine/Desktop/VRP.csv’  # Replace with your data file path
   ```

### Running Optimization

Run the main program directly:

```bash
python vrp_optimization.py
```

The program will perform the following steps:
1. Load and preprocess data
2. Run weighted single-objective genetic algorithm
3. Run NSGA-II multi-objective optimization algorithm
4. Output results and generate visualization charts
5. Save Pareto frontier results to CSV file

## Algorithm Parameter Configuration

Adjust the following parameters in the configuration section of the code:

```python
POP_SIZE = 120        # Population size
NGEN = 200            # Number of iterations
CX_PB = 0.8           # Crossover probability
MUT_PB = 0.2          # Mutation probability
RANDOM_SEED = 42      # Random seed
WEIGHT_W = 0.3        # Weighting coefficient, balancing two objectives
```

## Code Structure

### 1. Configuration and Data Loading

- Load CSV data file
- Extract coordinates, efficiency, and demand information
- Identify warehouse locations
- Compute distance matrix

### 2. Single-Path Logic

- `routes_from_individual`: Convert genetic algorithm individuals into actual paths
- `compute_f1`: Calculate total travel distance
- `compute_f2`: Calculate total efficiency

### 3. DEAP Framework Setup

- Create fitness function and individual types
- Register genetic algorithm operations (initialization, crossover, mutation, selection)
- Define evaluation function

### 4. Run Functions

- `run_weighted_ga`: Execute weighted single-objective genetic algorithm
- `run_nsga2`: Execute NSGA-II multi-objective optimization algorithm

### 5. Visualization

- `plot_routes`: Plot optimized paths
- `plot_pareto`: Plot Pareto front

### 6. Main Program

- Execute both algorithms
- Output results
- Generate visualization charts
- Save Pareto frontier results

## Result Interpretation

### Weighted Single-Objective Genetic Algorithm

- Output f₁ and f₂ values for all individuals
- Display optimal individual's path and objective values
- Plot optimal path diagram

### NSGA-II Multi-Objective Optimization Algorithm

- Outputs all non-dominated solutions on the Pareto frontier
- Identifies and displays the individual with the minimum f₁ value
- Plots the path map for that individual
- Saves Pareto frontier results to a CSV file

## Comparison of the Two Methods

### Weighted Single-Objective Genetic Algorithm

### NSGA-II Multi-Objective Optimization Algorithm

Translated with DeepL.com (free version)
