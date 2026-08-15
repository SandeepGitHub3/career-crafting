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
![Uploading image.png…]()


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
