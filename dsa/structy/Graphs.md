# Graphs

## Topic: Basic Graph Traversal

1. **Depth-First Search (DFS)**
   - Complexity: O(V + E)
   - Description: Explore as far as possible along each branch before backtracking.

2. **Breadth-First Search (BFS)**
   - Complexity: O(V + E)
   - Description: Explore all neighbors at the present depth prior to moving on to nodes at the next depth level.

## Topic: Shortest Path Problems

1. **Dijkstra's Algorithm**
   - Complexity: O(E + V log V)
   - Description: Finds the shortest path between nodes in a weighted graph.

2. **Bellman-Ford Algorithm**
   - Complexity: O(VE)
   - Description: Computes shortest paths from a single source vertex to all vertices.

3. **A* Search Algorithm**
   - Complexity: O(E)
   - Description: Finds the shortest path in weighted graphs with heuristics.

## Topic: Connectivity Problems

1. **Connected Components**
   - Complexity: O(V + E)
   - Description: Identify all connected components in an undirected graph.

2. **Cycle Detection**
   - Complexity: O(V + E)
   - Description: Check if a graph has a cycle.

## Topic: Minimum Spanning Tree

1. **Kruskal's Algorithm**
   - Complexity: O(E log E)
   - Description: Finds the minimum spanning tree for a connected graph.

2. **Prim's Algorithm**
   - Complexity: O(E + V log V)
   - Description: Another method for finding the minimum spanning tree using priority queues.

## Topic: Advanced Graph Algorithms

1. **Topological Sort**
   - Complexity: O(V + E)
   - Description: Order vertices in a directed acyclic graph (DAG).

2. **Floyd-Warshall Algorithm**
   - Complexity: O(V^3)
   - Description: Find shortest paths in a weighted graph with positive or negative edge weights.

## Topic: Problem Solving and Applications

1. **Finding Strongly Connected Components**
   - Complexity: O(V + E)
   - Description: Identifies strongly connected components in directed graphs using Kosaraju’s algorithm.

2. **Graph Coloring**
   - Complexity: O(V + E)
   - Description: Assigns different colors to vertices of a graph such that no two adjacent vertices share the same color.