<h1>Problems</h1>
  
<h3>1. knapsack</h3>

- Problem Statement 
<img width="734" height="268" alt="image" src="https://github.com/user-attachments/assets/f22487dd-aa0b-47fb-8a28-608e56c14b0d" />

  
- Approach - Recursive decision tress with Bases cases
<img width="649" height="329" alt="image" src="https://github.com/user-attachments/assets/525400d6-ebfb-4f34-b06a-931834df5b96" />

- Time and Space Complexity
<img width="674" height="390" alt="image" src="https://github.com/user-attachments/assets/fb59603c-211a-4c06-a671-976d6351bf59" />

- Solution
```
class Source {
  public static double knapsack(List<Integer> values, List<Integer> weights, int weightLimit, int i, HashMap<List<Integer>, Double> memo) {
    if (weightLimit < 0) {
      return Double.NEGATIVE_INFINITY;
    }

    if (i == values.size()) {
      return 0;
    }

    List<Integer> key = List.of(weightLimit, i);
    if (memo.containsKey(key)) {
      return memo.get(key);
    }
    
    Double result = Math.max(
      values.get(i) + knapsack(values, weights, weightLimit - weights.get(i), i + 1, memo),
      knapsack(values, weights, weightLimit, i + 1, memo)
    );
    memo.put(key, result);
    return result;
  }
  
  public static int knapsack(List<Integer> values, List<Integer> weights, int weightLimit) {
    return (int) knapsack(values, weights, weightLimit, 0, new HashMap<>());
  }
}


- n = number of items 
- w = weight limit
- Time: O(nw)
- Space: O(nw)
```

2. 
