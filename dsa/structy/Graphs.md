# Graphs Fundamentals

Graphs are abstract data types that represent a set of objects (called vertices or nodes) connected by links (called edges). They are used to model pairwise relations between objects.

## Basics of Graphs
- **Vertex (Node)**: Fundamental unit by which graphs are formed.
- **Edge**: Connection between two vertices.
- **Directed Graph**: Graph where edges have a direction.
- **Undirected Graph**: Graph where edges do not have a direction.
- **Weighted Graph**: Graph where edges have weights/costs associated with them.
- **Unweighted Graph**: Graph where edges have no weights.

## Types of Graphs
1. **Simple Graph**: A graph without loops or multiple edges.
2. **Complete Graph**: A graph where every pair of vertices is connected.
3. **Bipartite Graph**: A graph that can be divided into two sets of vertices, with edges only between the sets.
4. **Cyclic and Acyclic Graph**: Graphs that contain cycles vs those that do not.
5. **Planar Graph**: A graph that can be drawn on a plane without edges crossing.

## Traversal Techniques
- **Depth-First Search (DFS)**: Explores as far as possible along each branch before backtracking.
- **Breadth-First Search (BFS)**: Explores all neighbors at the present depth prior to moving on to nodes at the next depth level.

# 20 Graph Problems Organized by Topic

## Pathfinding Problems
1. **Shortest Path in a Weighted Graph**: Use Dijkstra’s algorithm.
   ![Shortest Path Image](images/shortest_path.png)

2. **Path Between Two Nodes**: Check if a path exists between two nodes.
   ![Path Image](images/path_between_nodes.png)

## Graph Connectivity Problems
3. **Connected Components**: Identify all connected components in a graph.
   ![Connected Components](images/connected_components.png)

4. **Cycle Detection**: Determine if a graph has cycles.
   ![Cycle Detection](images/cycle_detection.png)

## Graph Traversal Problems
5. **Implement DFS and BFS**: Write functions for both traversal techniques.
   ![DFS BFS](images/dfs_bfs.png)

6. **Topological Sorting**: Order vertices in a directed acyclic graph.
   ![Topological Sorting](images/topological_sort.png)

## Miscellaneous Problems
7. **Minimum Spanning Tree**: Find MST using Prim's or Kruskal's algorithm.
   ![Minimum Spanning Tree](images/minimum_spanning_tree.png)

8. **Graph Coloring**: Color the graph using minimum colors so that no two adjacent vertices share the same color.
   ![Graph Coloring](images/graph_coloring.png)

9. **Eulerian Path**: Determine if a path traverses every edge exactly once.
   ![Eulerian Path](images/eulerian_path.png)

10. **Hamiltonian Path**: Determine if a path visits every vertex exactly once.
   ![Hamiltonian Path](images/hamiltonian_path.png)

## Advanced Graph Problems
11. **Network Flow**: Determine the maximum flow in a flow network.
   ![Network Flow](images/network_flow.png)

12. **Bipartite Check**: Check if a graph is bipartite.
   ![Bipartite Check](images/bipartite_check.png)

13. **Strongly Connected Components**: Find all strongly connected components in a directed graph.
   ![Strongly Connected](images/strongly_connected.png)

14. **Graph Isomorphism**: Determine if two graphs are isomorphic.
   ![Graph Isomorphism](images/graph_isomorphism.png)

15. **Shortest Cycle**: Find the shortest cycle in a graph.
   ![Shortest Cycle](images/shortest_cycle.png)

16. **Dynamic Connectivity**: Maintain connectivity information under edge updates.
   ![Dynamic Connectivity](images/dynamic_connectivity.png)

17. **Traveling Salesman Problem**: Solve TSP with different heuristics.
   ![TSP](images/tsp.png)

18. **Finding Bridges**: Identify bridges that, if removed, increase the number of connected components.
   ![Finding Bridges](images/finding_bridges.png)

19. **Articulation Points**: Identify points that, when removed, increase the number of connected components.
   ![Articulation Points](images/articulation_points.png)

20. **Maximum Cliques**: Find the largest clique in a graph.
   ![Maximum Cliques](images/maximum_cliques.png)
