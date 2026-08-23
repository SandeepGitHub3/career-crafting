### Intro

- Nodes also know as Vertices. 
<img width="375" height="455" alt="image" src="https://github.com/user-attachments/assets/ad72e192-5ee1-4e3a-913b-da25588564de" />

<img width="692" height="428" alt="image" src="https://github.com/user-attachments/assets/1958f552-085b-4229-86dd-8b481aa0ad34" />

Graph representation:  
<img width="731" height="446" alt="image" src="https://github.com/user-attachments/assets/0e761ea8-e92a-46e5-ac0f-dfe435e47c16" />

Building Adjacency list from List of edges
```
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

Traversal:  
<img width="669" height="536" alt="image" src="https://github.com/user-attachments/assets/325b15b8-6ac9-4665-bf5f-dde26b103f4c" />

DFS:  
<img width="595" height="522" alt="image" src="https://github.com/user-attachments/assets/1b4d772c-2761-4d8e-85ed-fe45eb6d908b" />

DFS Template:  
```
public static void depthFirstPrintIterative(Map<String, List<String>> graph, String src) {
    Stack<String> stack = new Stack<>();
    stack.push(src);

    while(!stack.isEmpty()) {
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

BFS:  
<img width="641" height="462" alt="image" src="https://github.com/user-attachments/assets/77815d01-4bef-46bb-9c4e-e80690bb79a6" />

BFS Template:  
```
public static void breadthFirstPrint(Map<String, List<String>> graph, String src) {
    ArrayDeque<String> queue = new ArrayDeque<>();
    queue.add(src);

    while(!queue.isEmpty()) {
      String node = queue.remove();
      System.out.println(node);
      for (String neighbor : graph.get(node)) {
        queue.add(neighbor);
      }
    }
  }
```

Nodes & Edges. 
No of edges = O(N^2) in worst case.    

<img width="1088" height="457" alt="image" src="https://github.com/user-attachments/assets/7e7475f5-9ba0-4a82-b23c-c2d76bbd78fc" />. 
<img width="430" height="164" alt="image" src="https://github.com/user-attachments/assets/8e5dac70-6052-412b-9183-c1a0d4bc2c86" />


### Problems
#### has path - directed acyclic graph

IMP - 
- Directed graph (acyclic): no cycles possible, so no visited set needed.
- Undirected graph: edges go both ways, so you can bounce back to the same node — need a visited set to avoid infinite loops.  

<img width="561" height="361" alt="image" src="https://github.com/user-attachments/assets/f6eebcb1-7e09-423a-8d0b-fbff7a70e3a0" />

Could use either DFS or BFS.   
<img width="382" height="265" alt="image" src="https://github.com/user-attachments/assets/d9cec061-776a-4f37-9e6f-55a46bf4384d" />

```
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

#### has path - undirectedPath graph

Since we could have cycle , we need to keep a track of visited nodes and make sure we do not visit them again. 
<img width="259" height="295" alt="image" src="https://github.com/user-attachments/assets/81000b4f-cad6-4b37-ba0c-0547a02da0b7" />. 
<img width="454" height="333" alt="image" src="https://github.com/user-attachments/assets/fc9886e3-7e00-4db2-9aa7-a67f4b1975b5" />. 

```
public static boolean undirectedPath(List<List<String>> edges, String nodeA, String nodeB) {
    return hasPath(buildGraph(edges),nodeA,nodeB, new HashSet<>());
  }

  public static boolean hasPath(Map<String, List<String>> graph, String nodeA, String nodeB, Set<String> visited) {
    if(nodeA.equals(nodeB)) return true;

    if(visited.contains(nodeA)) return false;

    visited.add(nodeA);
    for(String neighbour: graph.get(nodeA)){
      if(hasPath(graph,neighbour,nodeB, visited)){
        return true;
      }
    }
    return false;
  }


  private static Map<String, List<String>> buildGraph(List<List<String>> edges){
    Map<String, List<String>> graph = new HashMap<>();

    for(List<String> edge: edges){
      if(!graph.containsKey(edge.get(0))) graph.put(edge.get(0), new ArrayList<>());
      if(!graph.containsKey(edge.get(1))) graph.put(edge.get(1), new ArrayList<>());

      graph.get(edge.get(0)).add(edge.get(1));
      graph.get(edge.get(1)).add(edge.get(0));
    }
    
    return graph;
  }

// n = number of nodes
// e = number edges
// Time: O(e)
// Space: O(e)
```

### connected components count. 
- **Iterate** and **Traverse** through the nodes using DFS or BFS and keep track of visited nodes and count.   

<img width="476" height="300" alt="image" src="https://github.com/user-attachments/assets/0f634eaf-11b0-443f-aab4-0ce6b26d5ca1" />. 
<img width="543" height="330" alt="image" src="https://github.com/user-attachments/assets/c6e40740-914f-4634-a7d8-b2aca2daa8f3" />. 

```
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

#### largest component. 
<img width="436" height="351" alt="image" src="https://github.com/user-attachments/assets/be022537-39ac-42b2-ba78-1c9f1785b340" />. 



```
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

### shortest path in undirected graph
 - Use BFS for Shortest path Algos.

<img width="410" height="228" alt="image" src="https://github.com/user-attachments/assets/98247706-cfb8-4148-8ec6-ddcf3a7976a9" />. 

```
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

// e = number edges
// Time: O(e)
// Space: O(e)
```

### island count

```
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

<img width="507" height="332" alt="image" src="https://github.com/user-attachments/assets/fbfa6c5b-4272-4735-9417-045188f201b6" />. 

- Use be solved using Both DFS and BFS

```
public static int islandCount(List<List<String>> grid) {
    int count = 0; 
    Set<String> visited = new HashSet<>();
    
    for(int i=0 ; i<grid.size(); i++) {
      for(int j=0 ; j<grid.get(i).size(); j++){
        if(grid.get(i).get(j) == "L" && !visited.contains(getKey(i,j) )){
          count = count+ 1;
          dfs(grid,i,j,visited);
        }
      }
    }
    
    return count;
  }

  private static void dfs(List<List<String>> grid, int r, int c, Set<String> visited){
    if( r<0 || c<0 || r >= grid.size() || c >= grid.get(r).size()) return;
    if( grid.get(r).get(c) == "W") return;
    String key = getKey(r,c);
    if(visited.contains(key)) return;
    visited.add(key);

    dfs(grid,r+1,c,visited);
    dfs(grid,r-1,c,visited);
    dfs(grid,r,c+1,visited);
    dfs(grid,r,c-1,visited);

    return;
  }

  private static String getKey(int i, int j){
    return i+"---"+j;
  }

// r = number of rows
// c = number of columns
// Time: O(rc)
// Space: O(rc)
```

### minimum island

<img width="359" height="246" alt="image" src="https://github.com/user-attachments/assets/92118a9f-1bc4-41b4-b336-bc4d5048d026" />. 

```
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











