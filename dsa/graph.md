# Graph DSA — Interview Revision Notes

## 📌 Topic 1 — Graph Representations

### Intuition
- **Adjacency List** = phonebook — each node stores only its direct neighbours. Compact.
- **Adjacency Matrix** = full grid — every node-pair tracked. Instant edge lookup, wastes space.

### Key Facts
- 99% of interview problems → use **adjacency list**
- Weighted graph → store `int[]` pairs `{neighbour, weight}` instead of just `neighbour`

### Complexity
| | Adjacency List | Adjacency Matrix |
|---|---|---|
| Space | O(V + E) | O(V²) |
| Check edge (u→v) | O(degree) | O(1) |
| Get all neighbours | O(degree) | O(V) |
| Best for | Sparse graphs | Dense graphs |

### Common Mistakes
1. Forgetting undirected = two directional edges (add both u→v and v→u)
2. Using matrix for sparse graphs — wastes memory
3. 0-indexed vs 1-indexed — always clarify before building

### Code Templates

```java
// Unweighted undirected
Map<Integer, List<Integer>> graph = new HashMap<>();
for (int i = 0; i < n; i++) graph.put(i, new ArrayList<>());
for (int[] e : edges) {
    graph.get(e[0]).add(e[1]);
    graph.get(e[1]).add(e[0]); // remove for directed
}

// Weighted directed
Map<Integer, List<int[]>> graph = new HashMap<>();
for (int i = 0; i < n; i++) graph.put(i, new ArrayList<>());
for (int[] e : edges) {
    // e = {u, v, weight}
    graph.get(e[0]).add(new int[]{e[1], e[2]});
}
```

### Interview Problems
| Problem | Pattern |
|---|---|
| Clone Graph (LC 133) | Build adj list from node references |
| Find the Town Judge (LC 997) | In-degree / out-degree tracking |
| Number of Provinces (LC 547) | Matrix → adj list → traverse |

---

## 📌 Topic 2 — Graph Terminology

### Key Terms
| Term | Meaning | Example |
|---|---|---|
| Undirected | Edges have no direction | Facebook friends |
| Directed (Digraph) | Edges have direction (u→v) | Twitter follows |
| Weighted | Edges have a cost | Road network |
| Cyclic | Contains at least one cycle | Circular dependency |
| Acyclic | No cycles | Family tree |
| DAG | Directed + Acyclic | Task scheduling |
| Connected | Every node reachable from any node | Single island |
| Connected Component | A maximal connected subgraph | Group of islands |
| In-degree | Edges coming INTO a node | Directed graphs |
| Out-degree | Edges going OUT of a node | Directed graphs |

### Key Facts
- A **tree** = connected acyclic undirected graph with V-1 edges
- In a DAG → **topological sort** is always possible
- V nodes + V-1 edges + connected = a tree

### The 3 Questions to Ask in Every Interview
1. Directed or undirected?
2. Weighted or unweighted?
3. Connected or multiple components?

### Common Mistakes
1. Confusing connected vs strongly connected (directed graphs)
2. Assuming input is always connected — always loop over all unvisited nodes
3. Missing that trees are special graphs — BFS/DFS apply directly

### Code Template — Count Components

```java
static int countComponents(Map<Integer, List<Integer>> graph, int n) {
    boolean[] visited = new boolean[n];
    int components = 0;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            dfs(graph, i, visited);
            components++;
        }
    }
    return components;
}
```

### Interview Problems
| Problem | Pattern |
|---|---|
| Number of Connected Components (LC 323) | Loop all nodes, count DFS starts |
| Find the Town Judge (LC 997) | In-degree = n-1, out-degree = 0 |
| Number of Islands (LC 200) | Grid = implicit graph, count components |

---

## 📌 Topic 3 — Building a Graph in Code

### Key Facts
- Always initialise all nodes before adding edges
- Undirected → add edge in both directions
- Directed → add edge in one direction only
- Weighted → store `{neighbour, weight}` as `int[]`

### Code Template

```java
// Standard build pattern
static Map<Integer, List<Integer>> buildGraph(int[][] edges, int n) {
    Map<Integer, List<Integer>> graph = new HashMap<>();
    for (int i = 0; i < n; i++) graph.put(i, new ArrayList<>());
    for (int[] e : edges) {
        graph.get(e[0]).add(e[1]);
        graph.get(e[1]).add(e[0]); // omit for directed
    }
    return graph;
}
```

---

## 📌 Topic 4 — BFS (Breadth First Search)

### Intuition
Drop a stone in a pond — ripples spread **level by level**.
BFS explores all neighbours before going deeper. Uses a **Queue (FIFO)**.

### When to Use BFS
- Shortest path in **unweighted** graph
- Level-order traversal
- "Minimum steps / hops to reach X"
- Multi-source spreading (fire, rotting oranges)

### Complexity
- **Time:** O(V + E)
- **Space:** O(V)

### Common Mistakes
1. Marking visited on POLL instead of on ADD → duplicates in queue → TLE
2. Forgetting disconnected graphs — loop over all nodes
3. Using BFS for weighted shortest path — use Dijkstra instead

### Core Template

```java
static void bfs(Map<Integer, List<Integer>> graph, int start, int n) {
    boolean[] visited = new boolean[n];
    Queue<Integer> queue = new LinkedList<>();

    visited[start] = true;      // mark on ADD, not on poll
    queue.offer(start);

    while (!queue.isEmpty()) {
        int node = queue.poll();
        System.out.print(node + " ");

        for (int neighbour : graph.get(node)) {
            if (!visited[neighbour]) {
                visited[neighbour] = true;
                queue.offer(neighbour);
            }
        }
    }
}
```

### Level-by-Level BFS

```java
while (!queue.isEmpty()) {
    int size = queue.size(); // snapshot current level
    for (int i = 0; i < size; i++) {
        int node = queue.poll();
        // process node
        for (int neighbour : graph.get(node)) {
            if (!visited[neighbour]) {
                visited[neighbour] = true;
                queue.offer(neighbour);
            }
        }
    }
    level++;
}
```

### Grid BFS Template

```java
int[][] dirs = {{0,1},{0,-1},{1,0},{-1,0}};
Queue<int[]> queue = new LinkedList<>();
visited[0][0] = true;
queue.offer(new int[]{0, 0});

while (!queue.isEmpty()) {
    int[] curr = queue.poll();
    int r = curr[0], c = curr[1];
    for (int[] dir : dirs) {
        int nr = r + dir[0], nc = c + dir[1];
        if (nr >= 0 && nr < rows && nc >= 0 && nc < cols
                && !visited[nr][nc] && grid[nr][nc] == 0) {
            visited[nr][nc] = true;
            queue.offer(new int[]{nr, nc});
        }
    }
}
```

### Interview Problems
| Problem | Pattern |
|---|---|
| Number of Islands (LC 200) | BFS on grid, count components |
| Rotting Oranges (LC 994) | Multi-source BFS, level = minutes |
| Shortest Path in Binary Matrix (LC 1091) | BFS on grid, return level count |

---

## 📌 Topic 5 — DFS (Depth First Search)

### Intuition
Exploring a maze — go as deep as possible, hit a dead end, backtrack, try next path.
Uses a **Stack** (or recursion call stack).

### When to Use DFS
- Path existence between two nodes
- Cycle detection
- Topological sort
- Connected components
- Backtracking (mazes, word search)
- Finding all paths

### Complexity
- **Time:** O(V + E)
- **Space:** O(V)

### Common Mistakes
1. Not marking visited BEFORE recursing → infinite loops in cyclic graphs
2. Stack overflow on large graphs — switch to iterative DFS
3. Iterative DFS processes neighbours in reverse order vs recursive

### Recursive DFS Template

```java
static void dfs(Map<Integer, List<Integer>> graph,
                int node, boolean[] visited) {
    visited[node] = true;
    System.out.print(node + " ");

    for (int neighbour : graph.get(node)) {
        if (!visited[neighbour]) {
            dfs(graph, neighbour, visited);
        }
    }
}
```

### Iterative DFS Template

```java
static void dfsIterative(Map<Integer, List<Integer>> graph,
                          int start, int n) {
    boolean[] visited = new boolean[n];
    Deque<Integer> stack = new ArrayDeque<>();
    stack.push(start);

    while (!stack.isEmpty()) {
        int node = stack.pop();
        if (visited[node]) continue;
        visited[node] = true;
        // process node
        for (int neighbour : graph.get(node)) {
            if (!visited[neighbour]) stack.push(neighbour);
        }
    }
}
```

### Find All Paths Template (with Backtracking)

```java
static void findAllPaths(Map<Integer, List<Integer>> graph,
                          int node, int target,
                          List<Integer> path,
                          List<List<Integer>> result) {
    path.add(node);
    if (node == target) {
        result.add(new ArrayList<>(path));
    } else {
        for (int neighbour : graph.get(node)) {
            if (!path.contains(neighbour)) {
                findAllPaths(graph, neighbour, target, path, result);
            }
        }
    }
    path.remove(path.size() - 1); // backtrack
}
```

### Grid DFS Template

```java
static void dfsGrid(int[][] grid, int r, int c, boolean[][] visited) {
    int rows = grid.length, cols = grid[0].length;
    if (r < 0 || r >= rows || c < 0 || c >= cols
            || visited[r][c] || grid[r][c] == 0) return;

    visited[r][c] = true;
    int[][] dirs = {{0,1},{0,-1},{1,0},{-1,0}};
    for (int[] dir : dirs) {
        dfsGrid(grid, r + dir[0], c + dir[1], visited);
    }
}
```

### Interview Problems
| Problem | Pattern |
|---|---|
| Number of Islands (LC 200) | DFS on grid, sink visited cells |
| Path Sum II (LC 113) | DFS + backtracking to find all paths |
| Word Search (LC 79) | DFS on grid with backtracking |

---

## 🆚 BFS vs DFS — Quick Comparison

| | BFS | DFS |
|---|---|---|
| Data structure | Queue | Stack / Recursion |
| Shortest path | ✅ Yes (unweighted) | ❌ No |
| Memory usage | More (stores level) | Less (stores path) |
| Best for | Shortest path, levels | Paths, cycles, backtracking |
| Grid problems | Shortest path in grid | Flood fill, connected area |

---

## ⚡ Master Cheat Sheet

### Build a graph
```java
Map<Integer, List<Integer>> g = new HashMap<>();
for (int i = 0; i < n; i++) g.put(i, new ArrayList<>());
for (int[] e : edges) { g.get(e[0]).add(e[1]); g.get(e[1]).add(e[0]); }
```

### BFS
```java
Queue<Integer> q = new LinkedList<>();
boolean[] vis = new boolean[n];
vis[start] = true; q.offer(start);
while (!q.isEmpty()) {
    int node = q.poll();
    for (int nb : g.get(node)) if (!vis[nb]) { vis[nb] = true; q.offer(nb); }
}
```

### DFS
```java
void dfs(int node, boolean[] vis) {
    vis[node] = true;
    for (int nb : g.get(node)) if (!vis[nb]) dfs(nb, vis);
}
```

### Count components
```java
int count = 0;
for (int i = 0; i < n; i++) if (!vis[i]) { dfs(i, vis); count++; }
```

### Grid directions
```java
int[][] dirs = {{0,1},{0,-1},{1,0},{-1,0}}; // 4-directional
int[][] dirs8 = {{0,1},{0,-1},{1,0},{-1,0},{1,1},{1,-1},{-1,1},{-1,-1}}; // 8-directional
```

---

*Notes will be updated as we complete more topics.*
