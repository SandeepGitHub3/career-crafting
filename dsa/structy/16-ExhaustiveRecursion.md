# Exhaustive Recursion - Difficult topic

### subsets
Write a method, subsets, that takes in a list as an argument. The method should return a 2D list where each subarray represents one of the possible subsets of the list.

The elements within the subsets and the subsets themselves may be returned in any order.

You may assume that the input list contains unique elements.

Source.subsets(List.of("a", "b")); // ->
// [ 
//   [], 
//   [ "b" ], 
//   [ "a" ], 
//   [ "a", "b" ] 
// ]

<img width="564" height="331" alt="image" src="https://github.com/user-attachments/assets/62e41bbe-930f-47c9-b764-6bfb8455ee4d" />
<img width="491" height="366" alt="image" src="https://github.com/user-attachments/assets/d7d83b0c-f00d-4ba3-b097-632d93f0baf6" />


```
public static List<List<String>> subsets(List<String> elements) {
    if(elements.size() == 0) return List.of(List.of());

    String ele = elements.get(0);
    List<List<String>> subsetsWithoutEle = subsets(elements.subList(1, elements.size()));
    List<List<String>> allSubsets = new ArrayList<>(subsetsWithoutEle);
    
    
    for(List<String> subsetWithoutEle : subsetsWithoutEle){
      List<String> subsetWithEle = new ArrayList<>(subsetWithoutEle);
      subsetWithEle.add(ele);
      allSubsets.add(subsetWithEle);
    }
    
    return allSubsets;
  }
```

### permutations
Write a method, permutations, that takes in a list an argument. The method should return a 2D list where each subarray represents one of the possible permutations of the list.

The subarrays may be returned in any order.

You may assume that the input list contains unique elements.

Source.permutations(List.of("a", "b", "c")); // -> 
// [ 
//   [ "a", "b", "c" ], 
//   [ "b", "a", "c" ], 
//   [ "b", "c", "a" ], 
//   [ "a", "c", "b" ], 
//   [ "c", "a", "b" ], 
//   [ "c", "b", "a" ] 
// ] 

<img width="412" height="195" alt="image" src="https://github.com/user-attachments/assets/c13cfde4-11f8-4e11-91e7-f0cf403a3311" />

```
public static List<List<String>> permutations(List<String> elements) {
    if(elements.size() == 0) return List.of(List.of());

    List<List<String>> allPerms = new ArrayList<>();

    String ele = elements.get(0); // a
    List<List<String>> subAllPerms = permutations(elements.subList(1,elements.size())); // [b,c]
    // --> No elements []
    // --> one element [c] ---[c]
    // --> 2 elements [b,c]           [c,b]
    // --> 3 elements 
    //                [a,b,c]        [a,c,b]
    //                [b,a,c]        [c,a,b]
    //                [b,c,a]        [c,b,a]

    for(List<String> subAllPerm: subAllPerms){
      for(int i=0;i<=subAllPerm.size(); i++){
        List<String> allPerm = new ArrayList<>();
        List<String> leftPerm = subAllPerm.subList(0,i);
        List<String> rigthPerm = subAllPerm.subList(i,subAllPerm.size());
        allPerm.addAll(leftPerm);
        allPerm.add(ele);
        allPerm.addAll(rigthPerm);
        allPerms.add(allPerm);
      }
    }
    return allPerms;
  }
```

#### Subsers & Permutations
Subsets- order does not matter - Total permuaions of n items -  2^n
Permuatations - Order does matter - Total permuaions of n items is n!


### create combinations
Write a method, createCombinations, that takes in a list and a length as arguments. The method should return a 2D list representing all of the combinations of the specified length.

The items within the combinations and the combinations themselves may be returned in any order.

You may assume that the input list contains unique elements and 1 <= k <= items.length.

Source.createCombinations(List.of("a", "b", "c"), 2); // ->
// [
//   [ "a", "b" ],
//   [ "a", "c" ],
//   [ "b", "c" ]
// ]

<img width="379" height="183" alt="image" src="https://github.com/user-attachments/assets/5c1c9567-e8e5-499d-ac7e-9cc6c4d70ded" />
<img width="382" height="145" alt="image" src="https://github.com/user-attachments/assets/3911658e-5376-4eca-9eaf-389ecf0bffeb" />
<img width="379" height="133" alt="image" src="https://github.com/user-attachments/assets/c64dcf87-15ba-4a61-b444-2a596dea4e87" />
<img width="366" height="222" alt="image" src="https://github.com/user-attachments/assets/be032ac2-ae56-4991-9593-bef89873870b" />
<img width="347" height="225" alt="image" src="https://github.com/user-attachments/assets/7e270865-9bad-4032-8be5-ce9bde86a894" />
<img width="500" height="258" alt="image" src="https://github.com/user-attachments/assets/1ec0b3cc-cf6f-4deb-9ed2-bc0243748095" />

```Time complexity - Just meorize 
n = length of items
k = target length
Time: ~O(n choose k)
Space: ~O(n choose k)
```
Note: "n Choose k" refers to the binomial coefficient.
<img width="379" height="125" alt="image" src="https://github.com/user-attachments/assets/b0ef6161-2d3e-4472-914e-020067728f4b" />

```
public static List<List<String>> createCombinations(List<String> items, int k) {
    //Base Cases:
    //If k == 0, means find combinations of length 0 so return [[]]
    if(k == 0) return List.of(List.of());
    //If no items we return empty list.
    if(items.size() == 0) return List.of();


    List<List<String>> allCombos = new ArrayList<>();
    String item = items.get(0);

    for(List<String> allSubCombo : createCombinations(items.subList(1,items.size()),k-1)){
        List<String> newSubCombo = new ArrayList<>(allSubCombo);
        newSubCombo.add(item);
        allCombos.add(newSubCombo);
    }

    allCombos.addAll(createCombinations(items.subList(1,items.size()),k));
    
    return allCombos;
  }
```
### grocery budget
Write a method, groceryBudget, that takes in groceryList and a number budget. Every item in groceryList is a pair containing the item name and price. Your method should return a 2D list of all possible ways to purchase items without spending more than the given budget.

The order of the items in the return value does not matter.

You cannot purchase an item more than once. You do not have to spend the budget fully.

- Same as last problem with minor tweak around budget

```
public static List<List<String>> groceryBudget(List<Map.Entry<String, Integer>> groceryList, int budget) {
    
    // base case: with nothing left to consider, the one valid plan is buying nothing
    if(groceryList.isEmpty()) return List.of(List.of());

   List<List<String>> allCombos = new ArrayList<>(); 
   Map.Entry<String, Integer> first = groceryList.get(0);
   List<Map.Entry<String, Integer>> rest = groceryList.subList(1, groceryList.size());


    // branch 1: buy this item — only legal if we can afford it
    if (first.getValue() <= budget) {
        for (List<String> combo : groceryBudget(rest, budget - first.getValue())) {
            List<String> withFirst = new ArrayList<>();
            withFirst.add(first.getKey());
            withFirst.addAll(combo);
            allCombos.add(withFirst);
        }
    }
    
    allCombos.addAll(groceryBudget(rest,budget));
    return allCombos;
  }

// n = # of groceries
// Time: ~O(2^n)
// Space: ~O(2^n)
```



### lining up
Write a method, liningUp, that takes in an list of people and a capacity number. We need to add people to the waitlist for a popular restaurant, but space is limited.

The method should return a 2D list containing all the possible orders by which the people can line up. A valid line must be filled up exactly to the capacity.

liningUp(List.of("autumn", "anj", "aud"), 2); // ->
// [ 
//   [ "autumn", "anj" ], 
//   [ "anj", "autumn" ], 
//   [ "autumn", "aud" ], 
//   [ "aud", "autumn" ], 
//   [ "anj", "aud" ], 
//   [ "aud", "anj" ] 
// ] 


2 Options 
1] Take the element and reduce the capacity
2] do not take the element
<img width="551" height="224" alt="image" src="https://github.com/user-attachments/assets/dccc53e1-93a0-4f61-866c-0e5dbbdc5723" />

The recursive case will return the lineup with capacity -1
<img width="561" height="263" alt="image" src="https://github.com/user-attachments/assets/4d00f3a0-8144-4fcb-a814-4e8dc77ee2d5" />

We then try to add the first element at all possible positions
<img width="214" height="221" alt="image" src="https://github.com/user-attachments/assets/35fd39e7-833f-4b26-ac3d-fb2e2d59e1a7" />

Similarly we get the result from Branch 2
<img width="360" height="250" alt="image" src="https://github.com/user-attachments/assets/69572e2a-7015-4c8c-8286-7a0f35082299" />

We combine both lists to get final Answer
<img width="343" height="303" alt="image" src="https://github.com/user-attachments/assets/f415438e-5e26-4709-a7dc-ada029784805" />

2 Important Base cases
<img width="526" height="352" alt="image" src="https://github.com/user-attachments/assets/46bdd788-703f-4fe8-90e9-e7e4bc61740a" />

Time and Space Complexity
<img width="634" height="246" alt="image" src="https://github.com/user-attachments/assets/49993882-e4fe-4515-bce4-7e864aa04317" />

```
public static List<List<String>> liningUp(List<String> people, int capacity) {
    //if capacity == 0  there is just one way to form the line i.e empty line.
    if(capacity == 0 ) return List.of(List.of());
    //Return Empty List as there is no Line we can generate if no people.
    if(people.size() == 0) return List.of(); 

    String p1 = people.get(0);
    List<List<String>> allLineUp = new ArrayList<>();

    List<String> restPeople = people.subList(1,people.size());
    allLineUp.addAll(liningUp(restPeople,capacity));

    for(List<String> subLineUp: liningUp(restPeople,capacity-1)){
      for(int i = 0 ;i<=subLineUp.size(); i++){
        List<String> newLineUp = new ArrayList<>(subLineUp);
        newLineUp.add(i,p1);
        
        allLineUp.add(newLineUp);
      }
    }
    
    return allLineUp;
  }
```

### possible paths
Write a method that takes in a graph adjacency list, a source node, and a destination node. The method should return a list containing all possible paths that travel between the source and destination.

You can assume that the graph is a DAG (directed-acyclic-graph).

Map<String, List<String>> graph = Map.of(
  "a", List.of("b", "c", "d"),
  "b", List.of("d"),
  "c", List.of("d"),
  "d", List.of()
);
possiblePaths(graph, "a", "d"); // ->
// [
//   ["a", "b", "d"],
//   ["a", "c", "d"],
//   ["a", "d"]
// ]

<img width="577" height="281" alt="image" src="https://github.com/user-attachments/assets/f20359a8-306b-412b-82ac-07472d811f01" />
<img width="501" height="344" alt="image" src="https://github.com/user-attachments/assets/cd18469f-b648-4385-860c-1eddca597bf4" />
<img width="466" height="339" alt="image" src="https://github.com/user-attachments/assets/e5203b7e-33f0-47e6-b30c-ade3885c1ca2" />
<img width="447" height="295" alt="image" src="https://github.com/user-attachments/assets/d547c601-895c-40c5-9a81-8f49a34a2836" />
<img width="619" height="358" alt="image" src="https://github.com/user-attachments/assets/712e5fa7-43e8-4b2f-b6e1-aa8044833c86" />

```
public static List<List<String>> possiblePaths(Map<String, List<String>> graph, String src, String dst) {
    if(src.equals(dst)) return List.of(List.of(dst));
    if(graph.get(src).isEmpty()) return List.of();

    List<List<String>> allPossiblePaths = new ArrayList<>();

    for(String neighbour : graph.get(src)){
      List<List<String>> neighbourPaths = possiblePaths(graph,neighbour,dst);
      for(List<String> neighbourPath: neighbourPaths){
        List<String> path = new ArrayList<>();
        path.add(src);
        path.addAll(neighbourPath);
        allPossiblePaths.add(path);
      }
    }
    
    return allPossiblePaths;
  }
```


### parenthetical possibilities
Write a method, parentheticalPossibilities, that takes in a string as an argument. The method should return a list containing all of the strings that could be generated by expanding all parentheses of the string into its possibilities.

Source.parentheticalPossibilities("x(mn)yz"); // -> 
// [ "xmyz", "xnyz" ]

Source.parentheticalPossibilities("(qr)ab(stu)c"); // ->
// [ "qabsc", "qabtc", "qabuc", "rabsc", "rabtc", "rabuc" ]


<img width="437" height="342" alt="image" src="https://github.com/user-attachments/assets/b0c47208-2419-42b6-a427-f0fa93a234d1" />
<img width="386" height="323" alt="image" src="https://github.com/user-attachments/assets/8a06a7ed-71e1-4c60-bf36-6f17dec0be3c" />
<img width="374" height="393" alt="image" src="https://github.com/user-attachments/assets/757a25cb-b3b7-4827-bf78-6af4bc9bae09" />
<img width="177" height="117" alt="image" src="https://github.com/user-attachments/assets/87eb24e7-e776-4779-b70a-c747a4358867" />

```
    public static List<String> parentheticalPossibilities(String s) {
        List<String> allPossibilities = new ArrayList<>();
    
        int open = s.indexOf('(');
        if(open == -1){
          allPossibilities.add(s);
          return allPossibilities;
        }
    
        int close = s.indexOf(')',open);
        String prefix = s.substring(0,open);
        String group = s.substring(open+1,close);
        String suffix = s.substring(close+1);
        
        for(String suffixString: parentheticalPossibilities(suffix)){
          for(char c: group.toCharArray()){
            allPossibilities.add(prefix+c+suffixString);
          }
        }
        
        return allPossibilities;
  }
```










