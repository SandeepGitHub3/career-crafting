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





