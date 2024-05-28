# Ghosts in the Maze

## Overview

This project aims to give you hands-on experience with search algorithms by solving a problem within a dynamically changing environment. You'll create an environment, develop an agent to navigate through it, and analyze the performance of your agent as it interacts with the environment.

## Project Goals

1. **Implement Search Algorithms**: Gain experience in developing and using search algorithms to solve practical problems.
2. **Highlight Planning vs. Execution**: Understand the difference between planning a strategy and executing it in a changing environment.
3. **Analyze Agent Performance**: Collect and analyze data to evaluate how well your agent accomplishes its goals.

## 1. Implementation

### 1.1 The Environment

The environment is a maze-like square grid (51x51). The cells in the grid can either be open (unblocked) or obstructed (blocked). The goal is to generate numerous mazes to test the agent. Here's how:

1. **Grid Generation**: Start with an empty 51x51 grid.
2. **Random Blockage**: Iterate through each cell, making it blocked with a probability of 0.28 and unblocked with a probability of 0.72.
3. **Quality Check**: Ensure the maze is navigable:
   - Remove blocks from the upper left and lower right corners.
   - Confirm there is a path from the upper left to the lower right corner using a pathfinding algorithm (e.g., BFS or DFS).
4. **Automate Maze Generation**: Automate this process to generate multiple valid mazes for testing.

### 1.2 The Agent

The agent starts in the upper left corner and aims to reach the lower right corner, navigating through unblocked cells. The agent can see the entire maze and plan its path accordingly.

### 1.3 The Problem: Ghosts

Ghosts are randomly placed in the maze and can pass through walls. The agent must avoid these ghosts, which move according to specific rules:

- **Movement Rules**:
  - Each ghost picks a neighboring cell (up, down, left, right).
  - If the neighbor is unblocked, the ghost moves there.
  - If the neighbor is blocked, the ghost either stays or moves into the blocked cell with equal probability.

If the agent encounters a ghost (or vice versa), the agent dies.

### 1.4 The Strategies

You will implement and compare various strategies for the agent to navigate the maze:

#### Agent 1: The Ignorant Navigator

- **Strategy**: Plans the shortest path and follows it, ignoring the ghosts.
- **Characteristics**: Simple and efficient in static environments but vulnerable to dynamic changes (ghosts).

#### Agent 2: The Replanner

- **Strategy**: Replans the path at every step based on the current positions of the ghosts.
- **Characteristics**: Adaptable to changes but computationally expensive due to constant replanning.

#### Agent 3: The Forecaster

- **Strategy**: Considers all possible moves and simulates future states based on the rules of Agent 2.
- **Characteristics**: Balances between adaptation and foresight, choosing moves with the highest survival probability.

#### Agent 4: The Innovator

- **Strategy**: Develop your own strategy to outperform Agent 3.
- **Characteristics**: Innovative approach that balances efficiency and intelligence. It should consider both the shortest path and ghost proximity.
