### Intro

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







