# Part 1- Ghosts in the Maze

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


# Part 2- The Circle of Life

## Overview

The objective of this project is to develop a probabilistic model in an environment with uncertainty to guide decision-making processes. You will create an agent that pursues a prey while avoiding a predator. This project will challenge you to make informed decisions based on incomplete information about the locations of the prey and the predator.

## 1. The Environment

The environment is a graph of 50 nodes, numbered 1 to 50, connected in a large circle. Additional edges are randomly added to increase connectivity, ensuring each node has a degree of at least 3:

1. **Random Node Selection**: Select a random node with a degree less than 3.
2. **Add Edges**: Add an edge between the selected node and one of its neighbors within 5 steps forward or backward along the circle (e.g., node 10 might connect to node 7 or node 15, but not node 16).
3. **Stop When Complete**: Repeat the process until no more edges can be added.

**Graph Theory Question**: You can add at most 25 additional edges. Why? Are you always able to add this many? If not, what’s the smallest number of edges you’re always able to add?

## 2. The Predator, The Prey, and You

This environment is occupied by three entities:

1. **The Agent**: Wants to catch the Prey while avoiding the Predator.
2. **The Prey**: Moves randomly among its neighbors or stays in its current node.
3. **The Predator**: Moves towards the Agent, selecting the shortest path.

### Movement Rules

- **Agent**: Moves first.
- **Prey**: Moves randomly.
- **Predator**: Moves last, selecting the shortest path to the Agent.

## 3. Agents and Environments

Implement the following agents and analyze their performance. The starting positions of the Predator, Prey, and Agent are randomly selected, ensuring the Agent does not start on an occupied node.

### Complete Information Setting

**Agent 1**: Knows the exact positions of both the Predator and the Prey.

- **Movement Strategy**: Chooses neighbors based on:
  1. Closer to the Prey and farther from the Predator.
  2. Closer to the Prey and not closer to the Predator.
  3. Not farther from the Prey and farther from the Predator.
  4. Not farther from the Prey and not closer to the Predator.
  5. Farther from the Predator.
  6. Not closer to the Predator.
  7. Sit still and pray.

**Agent 2**: Design your own agent that outperforms Agent 1.

### Partial Prey Information Setting

**Agent 3**: Knows the Predator's position but not the Prey's. Can survey one node per move to gather information about the Prey.

- **Belief State Update**: Track and update the probabilities for each node based on known information and actions.
- **Movement Strategy**: Survey the node with the highest probability of containing the Prey. Then, assume the Prey is at the most probable node and move accordingly, following Agent 1's rules.

**Agent 4**: Design your own agent that outperforms Agent 3.

### Partial Predator Information Setting

**Agent 5**: Knows the Prey's position but not the Predator's. Can survey one node per move to gather information about the Predator.

- **Belief State Update**: Track and update the probabilities for each node based on known information and actions.
- **Movement Strategy**: Survey the node with the highest probability of containing the Predator, prioritize proximity. Then, assume the Predator is at the most probable node and move accordingly, following Agent 1's rules.

**Agent 6**: Design your own agent that outperforms Agent 5.

### Combined Partial Information Setting

**Agent 7**: Does not know the positions of the Predator or Prey initially. Can survey one node per move to gather information.

- **Belief State Update**: Track and update probabilities for both the Predator and Prey.
- **Movement Strategy**: Survey according to Agent 5’s rules if the Predator’s location is unknown, otherwise, follow Agent 3’s rules for the Prey. Act by assuming the positions of both entities at their respective most probable nodes.

**Agent 8**: Design your own agent that outperforms Agent 7.

## Questions to Consider

- What node should the Agent move towards, given its current information?
- What node should the Agent survey, given its current information?
- How best can the Agent use all available knowledge to make a decision?

# Part 3- Better, Smarter, Faster

## Overview

In this project, you will extend the environment from Project 2 to develop an agent that captures the prey as efficiently as possible. The environment consists of 50 nodes arranged in a circle with additional random edges. You will implement and evaluate different agent strategies, calculate the optimal number of moves required to catch the prey, and use machine learning to predict these values under various conditions.

## 1. Environment and State Space

### Environment Setup

- **Nodes**: 50 nodes arranged in a circle.
- **Edges**: Additional random edges to ensure connectivity.
- **Entities**: The Predator, the Prey, and the Agent.

### State Space

- **States**: Each state \( s \) is a configuration of the positions of the Predator, Agent, and Prey.
- **Distinct States**: There are \( 50^3 = 125,000 \) possible states.

## 2. Optimal Utility Calculation

For a given state \( s \), let \( U^*(s) \) be the minimal expected number of rounds to catch the prey for an optimal agent.

### Key Questions

- **Easy States**: Identify states where \( U^* \) is straightforward to determine.
- **Relation**: How \( U^*(s) \) relates to \( U^* \) of other states and the agent's actions.

### Program Implementation

- **Objective**: Determine \( U^* \) for every state \( s \) and the optimal action for each state.
- **Algorithm Description**: Detail the steps taken to compute \( U^* \).

### Failure States

- **Capture Impossibility**: Identify starting states where the agent cannot capture the prey and explain the cause.

### Maximum Finite \( U^* \)

- **Largest \( U^* \)**: Find the state with the highest finite \( U^* \) and provide a visualization.

## 3. Agent Simulation and Comparison

- **Simulation**: Simulate the performance of an agent based on \( U^* \).
- **Comparison**: Compare this agent's performance (in terms of steps to capture the prey) with Agent 1 and Agent 2 from Project 2.

### Difference Analysis

- **State Choices**: Identify states where the \( U^* \) agent and Agents 1 or 2 make different choices.
- **Visualization and Explanation**: Visualize such states and explain the \( U^* \) agent's decision.

## 4. Predictive Model for \( U^* \)

### Model \( V \)

- **Representation**: How to represent the states \( s \) as input features for the model.
- **Model Type**: Specify the model type and training process.
- **Overfitting**: Address potential overfitting issues.
- **Accuracy**: Evaluate the model's accuracy.

### Simulation Based on \( V \)

- **Performance**: Compare the performance of an agent based on \( V \) with the \( U^* \) agent.

## 5. Partial Information Scenario

### Unknown Prey Position

- **Utility Estimation**: Use the expected utility based on probable prey positions.

\[
U_{\text{partial}}(s_{\text{agent}}, s_{\text{predator}}, p) = \sum_{s_{\text{prey}}} p_{s_{\text{prey}}} U^*(s_{\text{agent}}, s_{\text{predator}}, s_{\text{prey}})
\]

### Simulation and Comparison

- **Partial Information Agent**: Simulate an agent using \( U_{\text{partial}} \) and compare its performance with Agents 3 and 4 from Project 2.
- **Optimality**: Discuss whether the partial information agent is optimal.

## 6. Model \( V_{\text{partial}} \)

- **Representation**: Represent states \( s_{\text{agent}}, s_{\text{predator}}, p \) as model inputs.
- **Model Type**: Specify the model type and training process.
- **Overfitting**: Address potential overfitting issues.
- **Accuracy**: Evaluate \( V_{\text{partial}} \)'s accuracy.
- **Comparison with \( V \)**: Compare the accuracy of \( V_{\text{partial}} \) with using \( V \) in the partial information context.
- **Simulation Based on \( V_{\text{partial}} \)**: Compare the performance of an agent based on \( V_{\text{partial}} \) with the \( U_{\text{partial}} \) agent.

## Bonus Challenges

### Bonus 1: Actual Utility Prediction

- **Model Development**: Build a model to predict the actual utility of the \( U_{\text{partial}} \) agent.
- **Data Source**: Describe where you obtain the data.
- **Model Accuracy**: Evaluate the model's accuracy and compare it to the estimated \( U_{\text{partial}} \) values.

### Bonus 2: Optimal Partial Information Agent

- **Agent Design**: Develop an optimal partial information agent.
