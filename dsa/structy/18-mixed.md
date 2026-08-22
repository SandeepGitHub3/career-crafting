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
## 9. Positioning Plants

<img width="738" height="696" alt="Positioning Plants Problem" src="https://github.com/user-attachments/assets/d0404940-bb59-4bd8-b036-3ae595209596" />

---
### Recursion Tree - Brute Force approach
<img width="572" height="425" alt="Recursion Tree" src="https://github.com/user-attachments/assets/6aa2477e-cd8b-453b-9b2e-6927f6b9bd37" />

---
### Overlapping Subproblems

<img width="545" height="420" alt="Overlapping Subproblems 1" src="https://github.com/user-attachments/assets/edcadda0-86cc-47c8-972e-d01c03b748e4" />

<img width="517" height="425" alt="Overlapping Subproblems 2" src="https://github.com/user-attachments/assets/2853edc5-baeb-4442-bdb2-ffc587373f82" />

---

### Final Solution
<img width="953" height="461" alt="Solution" src="https://github.com/user-attachments/assets/e63ac178-c1e1-4998-9e9f-b44c3b330886" />

---
## 13. breaking boundaries

<img width="735" height="601" alt="image" src="https://github.com/user-attachments/assets/f281e17b-994d-45c5-8881-2a19a4403fc3" />

---
### Approach
<img src="https://github.com/user-attachments/assets/b2fa25cb-ab6c-48b8-8460-dfabfacd826c" /><br>
<img src="https://github.com/user-attachments/assets/e161e6b2-eb12-4195-b17b-ce83237f34b3" /><br>
<img src="https://github.com/user-attachments/assets/fe019352-b603-4120-827b-4139ac61123a" /><br>
<img src="https://github.com/user-attachments/assets/9e3897a8-0c8d-4cc6-876d-28393a011b69" />
---
### Final Solution
<img width="569" height="403" alt="image" src="https://github.com/user-attachments/assets/a10bd5a2-c510-470a-a849-b813fc51283a" />


 
