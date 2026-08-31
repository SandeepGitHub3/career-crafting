# Graphs — DSA Revision Notes

## Index

- [Intro](#intro)
  
**Problem list:**
 
1. [Has Path (Directed Acyclic Graph)](#1-has-path-directed-acyclic-graph)
2. [Has Path (Undirected Graph)](#2-has-path-undirected-graph)
3. [Connected Components Count](#3-connected-components-count)
4. [Largest Component](#4-largest-component)
5. [Shortest Path (Undirected Graph)](#5-shortest-path-undirected-graph)
6. [Island Count](#6-island-count)
7. [Minimum Island](#7-minimum-island)
8. [Closest Carrot](#8-closest-carrot)
9. [Best Bridge (Multi-source BFS)](#9-best-bridge-multi-source-bfs)
10. [Cycle Detection (Directed Graph)](#10-cycle-detection-directed-graph)
11. [Prereqs Possible](#11-prereqs-possible)

---

## Intro

### Nodes & Edges

- Nodes are also known as **vertices**.

<img width="375" height="455" alt="image" src="https://github.com/user-attachments/assets/ad72e192-5ee1-4e3a-913b-da25588564de" />

<img width="692" height="428" alt="image" src="https://github.com/user-attachments/assets/1958f552-085b-4229-86dd-8b481aa0ad34" />

### Graph Representation

<img width="731" height="446" alt="image" src="https://github.com/user-attachments/assets/0e761ea8-e92a-46e5-ac0f-dfe435e47c16" />

**Building an adjacency list from a list of edges:**

```java
public static Map<String, List<String>> buildGraph(List<List<String>> edges) {
    Map<String, List<String>> map = new HashMap<>();
    for (List<String> edge : edges) {
      String a = edge.get(0);
      String b = edge.get(1);
      if (!map.containsKey(a)) {
          map.put(a, new ArrayList<>());
      }
      if (!map.containsKey(b)) {
          map.put(b, new ArrayList<>());
      }
      map.get(a).add(b);
      map.get(b).add(a);
    }
    return map;
}
```

### Traversal

<img width="669" height="536" alt="image" src="https://github.com/user-attachments/assets/325b15b8-6ac9-4665-bf5f-dde26b103f4c" />

#### DFS

<img width="595" height="522" alt="image" src="https://github.com/user-attachments/assets/1b4d772c-2761-4d8e-85ed-fe45eb6d908b" />

```java
public static void depthFirstPrintIterative(Map<String, List<String>> graph, String src) {
    Stack<String> stack = new Stack<>();
    stack.push(src);

    while (!stack.isEmpty()) {
      String node = stack.pop();
      System.out.println(node);
      for (String neighbor : graph.get(node)) {
        stack.push(neighbor);
      }
    }
}

public static void depthFirstPrintRecursive(Map<String, List<String>> graph, String src) {
    System.out.println(src);
    for (String neighbor : graph.get(src)) {
      depthFirstPrintRecursive(graph, neighbor);
    }
}
```

#### BFS

<img width="641" height="462" alt="image" src="https://github.com/user-attachments/assets/77815d01-4bef-46bb-9c4e-e80690bb79a6" />

```java
public static void breadthFirstPrint(Map<String, List<String>> graph, String src) {
    ArrayDeque<String> queue = new ArrayDeque<>();
    queue.add(src);

    while (!queue.isEmpty()) {
      String node = queue.remove();
      System.out.println(node);
      for (String neighbor : graph.get(node)) {
        queue.add(neighbor);
      }
    }
}
```

### Nodes & Edges — Complexity

- Number of edges = O(N²) in the worst case.

<img width="1088" height="457" alt="image" src="https://github.com/user-attachments/assets/7e7475f5-9ba0-4a82-b23c-c2d76bbd78fc" />

<img width="430" height="164" alt="image" src="https://github.com/user-attachments/assets/8e5dac70-6052-412b-9183-c1a0d4bc2c86" />

---

## Problems

### 1. Has Path (Directed Acyclic Graph)

- Given a DAG's adjacency list and two nodes (`src`, `dst`), return whether a directed path exists from `src` to `dst`.
- Could be solved with either DFS or BFS.

**IMP:**
- Directed graph (acyclic): no cycles possible, so no visited set needed.
- Undirected graph: edges go both ways, so you can bounce back to the same node — need a visited set to avoid infinite loops.

<img width="561" height="361" alt="image" src="https://github.com/user-attachments/assets/f6eebcb1-7e09-423a-8d0b-fbff7a70e3a0" />

<img width="382" height="265" alt="image" src="https://github.com/user-attachments/assets/d9cec061-776a-4f37-9e6f-55a46bf4384d" />

```java
public static boolean hasPath(Map<String, List<String>> graph, String src, String dst) {
    if (src == dst) {
      return true;
    }
    for (String neighbor : graph.get(src)) {
      if (hasPath(graph, neighbor, dst)) {
        return true;
      }
    }
    return false;
}
```

---

### 2. Has Path (Undirected Graph)

- Given an edge list for an undirected graph and two nodes, return whether a path exists between them.
- Cycles are possible here, so a visited set is required to avoid revisiting nodes.

<img width="259" height="295" alt="image" src="https://github.com/user-attachments/assets/81000b4f-cad6-4b37-ba0c-0547a02da0b7" />

<img width="454" height="333" alt="image" src="https://github.com/user-attachments/assets/fc9886e3-7e00-4db2-9aa7-a67f4b1975b5" />

```java
public static boolean undirectedPath(List<List<String>> edges, String nodeA, String nodeB) {
    return hasPath(buildGraph(edges), nodeA, nodeB, new HashSet<>());
}

public static boolean hasPath(Map<String, List<String>> graph, String nodeA, String nodeB, Set<String> visited) {
    if (nodeA.equals(nodeB)) return true;
    if (visited.contains(nodeA)) return false;

    visited.add(nodeA);
    for (String neighbour : graph.get(nodeA)) {
      if (hasPath(graph, neighbour, nodeB, visited)) {
        return true;
      }
    }
    return false;
}

private static Map<String, List<String>> buildGraph(List<List<String>> edges) {
    Map<String, List<String>> graph = new HashMap<>();

    for (List<String> edge : edges) {
      if (!graph.containsKey(edge.get(0))) graph.put(edge.get(0), new ArrayList<>());
      if (!graph.containsKey(edge.get(1))) graph.put(edge.get(1), new ArrayList<>());

      graph.get(edge.get(0)).add(edge.get(1));
      graph.get(edge.get(1)).add(edge.get(0));
    }
    return graph;
}
```

**Complexity:** Time `O(e)`, Space `O(e)` (n = nodes, e = edges)

---

### 3. Connected Components Count

- Given an adjacency list, return the number of separate connected components in the graph.
- **Approach:** iterate over every node; traverse (DFS/BFS) from each unvisited node, incrementing a counter once per new component.

<img width="476" height="300" alt="image" src="https://github.com/user-attachments/assets/0f634eaf-11b0-443f-aab4-0ce6b26d5ca1" />

<img width="543" height="330" alt="image" src="https://github.com/user-attachments/assets/c6e40740-914f-4634-a7d8-b2aca2daa8f3" />

```java
public static int connectedComponentsCount(Map<Integer, List<Integer>> graph) {
    HashSet<Integer> visited = new HashSet<>();
    int count = 0;
    for (int node : graph.keySet()) {
      if (traverseComponent(graph, node, visited)) {
        count += 1;
      }
    }
    return count;
}

public static boolean traverseComponent(Map<Integer, List<Integer>> graph, int node, HashSet<Integer> visited) {
    if (visited.contains(node)) {
      return false;
    }
    visited.add(node);

    for (int neighbor : graph.get(node)) {
      traverseComponent(graph, neighbor, visited);
    }
    return true;
}
```

---

### 4. Largest Component

- Given an adjacency list, return the size (node count) of the largest connected component.
- Same traversal pattern as Connected Components Count, but the traversal returns a size instead of a boolean.

<img width="436" height="351" alt="image" src="https://github.com/user-attachments/assets/be022537-39ac-42b2-ba78-1c9f1785b340" />

```java
public static int largestComponent(Map<Integer, List<Integer>> graph) {
    HashSet<Integer> visited = new HashSet<>();
    int maxSize = 0;
    for (int node : graph.keySet()) {
      int size = traverseSize(graph, node, visited);
      if (size > maxSize) {
        maxSize = size;
      }
    }
    return maxSize;
}

public static int traverseSize(Map<Integer, List<Integer>> graph, int node, HashSet<Integer> visited) {
    if (visited.contains(node)) {
      return 0;
    }
    visited.add(node);

    int count = 1;
    for (int neighbor : graph.get(node)) {
      count += traverseSize(graph, neighbor, visited);
    }
    return count;
}
```

---

### 5. Shortest Path (Undirected Graph)

- Given an edge list and two nodes, return the length (number of edges) of the shortest path between them, or `-1` if unreachable.
- **Key rule:** use BFS for shortest-path problems (unweighted graphs) — DFS does not guarantee the shortest path.

<img width="410" height="228" alt="image" src="https://github.com/user-attachments/assets/98247706-cfb8-4148-8ec6-ddcf3a7976a9" />

```java
public static int shortestPath(List<List<String>> edges, String nodeA, String nodeB) {
    HashMap<String, List<String>> graph = buildGraph(edges);
    HashSet<String> visited = new HashSet<>();
    ArrayDeque<SimpleEntry<String, Integer>> queue = new ArrayDeque<>();
    queue.add(new SimpleEntry<>(nodeA, 0));
    visited.add(nodeA);

    while (!queue.isEmpty()) {
      SimpleEntry<String, Integer> entry = queue.remove();
      String node = entry.getKey();
      int distance = entry.getValue();

      if (node == nodeB) {
        return distance;
      }

      for (String neighbor : graph.get(node)) {
        if (!visited.contains(neighbor)) {
          queue.add(new SimpleEntry<>(neighbor, distance + 1));
          visited.add(neighbor);
        }
      }
    }
    return -1;
}
```

**Complexity:** Time `O(e)`, Space `O(e)`

---

### 6. Island Count

- Given a grid of `"W"` (water) and `"L"` (land), return the number of islands — 4-directionally connected regions of land.
- Can be solved with either DFS or BFS.

**Sample:**

```java
List<List<String>> grid = List.of(
  List.of("W", "L", "W", "W", "W"),
  List.of("W", "L", "W", "W", "W"),
  List.of("W", "W", "W", "L", "W"),
  List.of("W", "W", "L", "L", "W"),
  List.of("L", "W", "W", "L", "L"),
  List.of("L", "L", "W", "W", "W")
);

Source.islandCount(grid); // -> 3
```

<img width="507" height="332" alt="image" src="https://github.com/user-attachments/assets/fbfa6c5b-4272-4735-9417-045188f201b6" />

```java
public static int islandCount(List<List<String>> grid) {
    int count = 0;
    Set<String> visited = new HashSet<>();

    for (int i = 0; i < grid.size(); i++) {
      for (int j = 0; j < grid.get(i).size(); j++) {
        if (grid.get(i).get(j).equals("L") && !visited.contains(getKey(i, j))) {
          count = count + 1;
          dfs(grid, i, j, visited);
        }
      }
    }
    return count;
}

private static void dfs(List<List<String>> grid, int r, int c, Set<String> visited) {
    if (r < 0 || c < 0 || r >= grid.size() || c >= grid.get(r).size()) return;
    if (grid.get(r).get(c).equals("W")) return;
    String key = getKey(r, c);
    if (visited.contains(key)) return;
    visited.add(key);

    dfs(grid, r + 1, c, visited);
    dfs(grid, r - 1, c, visited);
    dfs(grid, r, c + 1, visited);
    dfs(grid, r, c - 1, visited);
}

private static String getKey(int i, int j) {
    return i + "---" + j;
}
```

**Complexity:** Time `O(r·c)`, Space `O(r·c)` (r = rows, c = columns)

---

### 7. Minimum Island

- Same grid setup as Island Count; return the size (cell count) of the smallest island.
- Grid is guaranteed to contain at least one island.
- **Bug to remember:** mark a cell visited *before* recursing into neighbors, not after — otherwise adjacent cells call each other back and forth forever (infinite recursion).

<img width="359" height="246" alt="image" src="https://github.com/user-attachments/assets/92118a9f-1bc4-41b4-b336-bc4d5048d026" />

```java
public static int minimumIsland(List<List<String>> grid) {
    Set<String> visited = new HashSet<>();
    int minSize = Integer.MAX_VALUE;

    for (int i = 0; i < grid.size(); i++) {
      for (int j = 0; j < grid.get(i).size(); j++) {
        if (grid.get(i).get(j).equals("L") && !visited.contains(getKey(i, j))) {
          int size = dfs(grid, i, j, visited);
          minSize = Math.min(minSize, size);
        }
      }
    }
    return minSize;
}

private static int dfs(List<List<String>> grid, int r, int c, Set<String> visited) {
    if (r < 0 || c < 0 || r >= grid.size() || c >= grid.get(r).size()) return 0;
    if (grid.get(r).get(c).equals("W")) return 0;
    String key = getKey(r, c);
    if (visited.contains(key)) return 0;
    visited.add(key); // mark before recursing

    return 1 + dfs(grid, r + 1, c, visited)
             + dfs(grid, r - 1, c, visited)
             + dfs(grid, r, c + 1, visited)
             + dfs(grid, r, c - 1, visited);
}

private static String getKey(int i, int j) {
    return i + "," + j;
}
```

---

### 8. Closest Carrot

- Given a grid of `"X"` (blocked), `"O"` (free), `"C"` (carrot), plus a starting row/col, return the minimum number of steps to reach a carrot, or `-1` if unreachable.
- Shortest-path-on-a-grid → BFS, not DFS.

<img width="242" height="261" alt="image" src="https://github.com/user-attachments/assets/4ae74866-bedc-4724-8dff-360d9e738c4a" />

<img width="490" height="285" alt="image" src="https://github.com/user-attachments/assets/58011f7e-6a9d-4eb5-99a6-0e89d0fb060c" />

```java
public static int closestCarrot(List<List<String>> grid, int startRow, int startCol) {
    int stepCount = 0;
    Set<List<Integer>> visited = new HashSet<>();
    Queue<List<Integer>> qu = new ArrayDeque<>();
    qu.add(List.of(startRow, startCol, 0));

    while (!qu.isEmpty()) {
      List<Integer> node = qu.remove();
      int r = node.get(0);
      int c = node.get(1);
      int count = node.get(2);

      if (r >= 0 && c >= 0 && r < grid.size() && c < grid.get(r).size()
          && !visited.contains(List.of(r, c)) && !grid.get(r).get(c).equals("X")) {
        visited.add(List.of(r, c));
        if (grid.get(r).get(c).equals("C")) return count;

        qu.add(List.of(r + 1, c, count + 1));
        qu.add(List.of(r - 1, c, count + 1));
        qu.add(List.of(r, c + 1, count + 1));
        qu.add(List.of(r, c - 1, count + 1));
      }
    }
    return -1;
}
```

---

### 9. Best Bridge (Multi-source BFS)

- Given a grid with exactly two islands (`"L"`/`"W"`), return the minimum-length bridge (number of water cells) needed to connect them. A bridge does not need to be a straight line.
- **IMP — Multi-source BFS:** flood-fill island 1 and seed the BFS queue with *all* of its cells at `dist = 0`, then expand outward through water as one wave until an unvisited land cell (island 2) is found.
- **Rule that avoids most bugs here:** check a neighbor's type (land vs. water) *before* deciding to mark/enqueue it — never mark visited first and check type later.

<img width="386" height="310" alt="image" src="https://github.com/user-attachments/assets/930beafe-e63d-41f7-8d6a-4a1ce1a3a988" />

<img width="387" height="300" alt="image" src="https://github.com/user-attachments/assets/e8080d9a-cc83-4b83-ab21-f465eb3d7397" />

```java
public static int bestBridge(List<List<String>> grid) {

    Set<List<Integer>> visited = new HashSet<>();
    Queue<List<Integer>> qu = new ArrayDeque<>();
    boolean foundFirst = false;

    for (int i = 0; i < grid.size() && !foundFirst; i++) {
      for (int j = 0; j < grid.get(i).size() && !foundFirst; j++) {
        if (grid.get(i).get(j).equals("L")) {
          markIsland(grid, i, j, visited, qu);
          foundFirst = true;
        }
      }
    }

    List<List<Integer>> deltas = List.of(
        List.of(1, 0),
        List.of(-1, 0),
        List.of(0, 1),
        List.of(0, -1)
    );

    // BFS outward through water; stop the moment a neighbor is unvisited land
    while (!qu.isEmpty()) {
      List<Integer> cell = qu.poll();
      int r = cell.get(0), c = cell.get(1), dist = cell.get(2);

      for (List<Integer> d : deltas) {
        int nr = r + d.get(0), nc = c + d.get(1);
        if (nr < 0 || nc < 0 || nr >= grid.size() || nc >= grid.get(nr).size()) continue;

        List<Integer> pos = List.of(nr, nc);
        if (visited.contains(pos)) continue;

        if (grid.get(nr).get(nc).equals("L")) return dist; // hit island 2

        visited.add(pos);
        qu.add(List.of(nr, nc, dist + 1));
      }
    }
    return -1; // unreachable, problem guarantees two islands
}

private static void markIsland(List<List<String>> grid, int r, int c, Set<List<Integer>> visited, Queue<List<Integer>> qu) {
    if (r < 0 || c < 0 || r >= grid.size() || c >= grid.get(r).size()) return;
    if (grid.get(r).get(c).equals("W")) return;
    if (visited.contains(List.of(r, c))) return;

    visited.add(List.of(r, c));
    qu.add(List.of(r, c, 0));

    markIsland(grid, r + 1, c, visited, qu);
    markIsland(grid, r - 1, c, visited, qu);
    markIsland(grid, r, c + 1, visited, qu);
    markIsland(grid, r, c - 1, visited, qu);
}
```

---

### 10. Cycle Detection (Directed Graph)

- Given a directed graph's adjacency list, return whether it contains a cycle.
- **Approach:** DFS with two sets — `visiting` (on the current recursion path) and `visited` (fully processed). A cycle exists if you re-encounter a node still in `visiting`.

<img width="540" height="293" alt="image" src="https://github.com/user-attachments/assets/dd2d1caa-258c-4763-81e8-aadbb06e299a" />

```java
public static boolean hasCycle(Map<String, List<String>> graph) {
    HashSet<String> visited = new HashSet<>();
    for (String node : graph.keySet()) {
      if (hasCycle(graph, node, new HashSet<>(), visited)) {
        return true;
      }
    }
    return false;
}

private static boolean hasCycle(Map<String, List<String>> graph, String node, HashSet<String> visiting, HashSet<String> visited) {
    if (visiting.contains(node)) return true; // cycle detected
    if (visited.contains(node)) return false;

    visiting.add(node);

    for (String neighbour : graph.get(node)) {
      if (hasCycle(graph, neighbour, visiting, visited)) {
        return true;
      }
    }

    visiting.remove(node);
    visited.add(node);
    return false;
}
```

**Complexity:** Time `O(e)`, Space `O(n)` (n = nodes, e = edges)

---

### 11. Prereqs Possible

- Given a number of courses `n` (ids `0` to `n-1`) and a list of prerequisites where `List.of(A, B)` means course `A` must be taken before course `B`, return whether it's possible to complete all courses.
- **Boils down to:** cycle detection in a directed graph — if the prerequisite graph has a cycle, it's impossible.

**Sample:**

```java
int numCourses = 6;
List<List<Integer>> prereqs = List.of(
  List.of(0, 1),
  List.of(2, 3),
  List.of(0, 2),
  List.of(1, 3),
  List.of(4, 5)
);
Source.prereqsPossible(numCourses, prereqs); // -> true
```

<img width="421" height="185" alt="image" src="https://github.com/user-attachments/assets/e783feb1-c7a8-4078-9b34-fdf95dbf4c8c" />

<img width="419" height="249" alt="image" src="https://github.com/user-attachments/assets/8b4fa85e-4d8c-4a8b-8394-7b9ebe7304e4" />

<img width="544" height="296" alt="image" src="https://github.com/user-attachments/assets/b2a365a4-ab3c-47ca-b27a-e6f5873fa143" />

```java
public static boolean prereqsPossible(int numCourses, List<List<Integer>> prereqs) {
    Map<Integer, List<Integer>> gr = buildGraph(numCourses, prereqs);
    HashSet<Integer> visited = new HashSet<>();

    for (int i = 0; i < numCourses; i++) {
      if (hasCycle(gr, i, new HashSet<>(), visited)) {
        return false;
      }
    }
    return true;
}

private static boolean hasCycle(Map<Integer, List<Integer>> gr, int node, HashSet<Integer> visiting, HashSet<Integer> visited) {
    if (visiting.contains(node)) return true;
    if (visited.contains(node)) return false;

    visiting.add(node);

    for (Integer neighbour : gr.get(node)) {
      if (hasCycle(gr, neighbour, visiting, visited)) {
        return true;
      }
    }
    visiting.remove(node);
    visited.add(node);
    return false;
}

private static Map<Integer, List<Integer>> buildGraph(int numCourses, List<List<Integer>> prereqs) {
    Map<Integer, List<Integer>> map = new HashMap<>();

    for (int i = 0; i < numCourses; i++) {
      map.put(i, new ArrayList<>());
    }
    for (List<Integer> prereq : prereqs) {
      map.get(prereq.get(0)).add(prereq.get(1));
    }
    return map;
}
```

### 12. knight attack

Source.knightAttack(8, 1, 1, 2, 2); // -> 2

- Use BFS to find the Shortest Path.
- Keep track of the no of steps.
  
- Possible Move Options for Knight. 
<img width="292" height="291" alt="image" src="https://github.com/user-attachments/assets/2f1ef622-f5bf-45ed-b7b8-921e43dd4f2b" />
<img width="469" height="345" alt="image" src="https://github.com/user-attachments/assets/480b8423-8869-4bd3-89ca-6da1de7833cf" />


```
public static int knightAttack(int n, int kr, int kc, int pr, int pc) {
    Queue<List<Integer>> qu = new ArrayDeque<>();
    Set<List<Integer>> visited = new HashSet<>();
    qu.add(List.of(kr,kc,0));

    List<List<Integer>> positions = List.of(
      List.of(1,2),
      List.of(-1,2),
      List.of(-1,-2),
      List.of(1,-2),
      List.of(2,1),
      List.of(-2,1),
      List.of(-2,-1),
      List.of(2,-1)
    );

    while(!qu.isEmpty()){
      List<Integer> node = qu.remove();
      int cKr = node.get(0);
      int cKc = node.get(1);
      int dist = node.get(2);

      if(cKr == pr && cKc == pc) return dist;

      for(List<Integer> pos : positions){
        int r = cKr + pos.get(0);
        int c = cKc + pos.get(1);
        if(!visited.contains(List.of(r,c)) && isWithinBounds(n,r,c)){
          qu.add(List.of(r,c,dist+1));
          visited.add(List.of(r,c));
        }  
      }
    }
    
    return -1;
  }

  private static boolean isWithinBounds(int n, int r, int c){
      if( r<0 || c<0 || r>=n || c>=n) return false;
      return true;
  }
```

### 13 can color - Bipartate Graphs

- Use Classic DFS

<img width="373" height="295" alt="image" src="https://github.com/user-attachments/assets/67e3dc22-d7fa-4317-9a06-caf6924de5d1" />

```  public static boolean canColor(Map<String, List<String>> graph) {
    Map<String,String> visited = new HashMap<>();
    
    for(String key: graph.keySet()){
       if(!visited.containsKey(key) &&!canColor(graph,key,"Red",visited))
          return false;   
    }
    return true;
  }

  private static boolean canColor(Map<String, List<String>> graph,String node, String color, Map<String,String> visited){
    
    if(visited.containsKey(node)){
      return visited.get(node).equals(color);
    }

    visited.put(node,color);

    String neighbourColor = color.equals("Red")? "Blue":"Red";
    
    for(String neighbour: graph.get(node)){
      if(!canColor(graph,neighbour,neighbourColor,visited))
        return false;
    }
    return true;
  }
// n = number of nodes
// Time: O(n^2)
// Space: O(n)
```

### 14 - tolerant teams - Bipartite

<img width="409" height="231" alt="image" src="https://github.com/user-attachments/assets/f72fb730-3bf1-40f0-acd2-fc3fa8b37326" />

<img width="430" height="397" alt="image" src="https://github.com/user-attachments/assets/cab04edc-a01d-4344-bda0-b530d6700eb9" />

```
Source.tolerantTeams(List.of(
  List.of("philip", "seb"),
  List.of("raj", "nader")
)); // -> true

```
- Same code as previous problem, just additonal step of converting the list of rivalries into Adjacency list.

### 15 - rare routing
Write a method, rareRouting, that takes in a number of cities (n) and a two dimensional List where each sublist represents a direct road that connects a pair of cities. The method should return a boolean indicating whether or not there exists a unique route for every pair of cities. A route is a sequence of roads that does not visit a city more than once.

Cities will be numbered 0 to n - 1.

You can assume that all roads are two-way roads. This means if there is a road between A and B, then you can use that road to go from A to B or go from B to A.  

- <img width="174" height="221" alt="image" src="https://github.com/user-attachments/assets/4f6d83a8-e980-4d9e-9853-4e04c20f8f9d" />.
- <img width="188" height="224" alt="image" src="https://github.com/user-attachments/assets/780ec737-a0f8-434d-8b72-49bcae1344ce" />.
- <img width="274" height="232" alt="image" src="https://github.com/user-attachments/assets/b94ac7ed-f5b0-4d8f-8b3d-5dd98f17f8d4" />
- Need to Keep track of Parent Node and make sure we do not revisit the Parent Node.
- <img width="192" height="228" alt="image" src="https://github.com/user-attachments/assets/a27575da-0d84-4cc5-98d0-b6bb7e560655" />.
- <img width="228" height="273" alt="image" src="https://github.com/user-attachments/assets/d743989d-2aa0-402e-b780-0f84976e960d" />.
- <img width="263" height="265" alt="image" src="https://github.com/user-attachments/assets/6f9da392-798f-4fa7-8feb-f16bc8eb5a9d" />.
- <img width="380" height="162" alt="image" src="https://github.com/user-attachments/assets/e043d06c-6ea4-4e37-bfde-3438b225f6a0" />.
- <img width="179" height="105" alt="image" src="https://github.com/user-attachments/assets/ac5cf5ac-f822-4af8-b88c-046f2145094f" />.

```
public static boolean rareRouting(int n, List<List<Integer>> roads) {
    HashMap<Integer, List<Integer>> graph = buildGraph(n, roads);
    HashSet<Integer> visited = new HashSet<>();
    boolean valid = validate(graph, 0, visited, -1);
    return valid && visited.size() == n;
  }
  
  public static boolean validate(HashMap<Integer, List<Integer>> graph, int node, HashSet<Integer> visited, int prevNode) {
    if (visited.contains(node)) {
      return false;
    }
    visited.add(node);
    
    for (int neighbor : graph.get(node)) {
      if(neighbor != prevNode && !validate(graph, neighbor, visited, node)) {
        return false;
      }
    }
    return true;
  }
  
  public static HashMap<Integer, List<Integer>> buildGraph(int numNodes, List<List<Integer>> edges)  {
    HashMap<Integer, List<Integer>> graph = new HashMap<>();
    for (int i = 0; i < numNodes; i += 1) {
      graph.put(i, new ArrayList<>());
    }
    
    for (List<Integer> pair : edges) {
      int nodeA = pair.get(0);
      int nodeB = pair.get(1);
      graph.get(nodeA).add(nodeB);
      graph.get(nodeB).add(nodeA);
    }
    return graph;
  }
```












