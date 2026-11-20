## Intro

<img width="820" height="476" alt="image" src="https://github.com/user-attachments/assets/0ea11e6c-822c-4fd6-b22d-2355c092b47b" />

### 1. Classic Binary Search
```
  public static int binarySearch(List<Integer> numbers, int target) {
    int start =0;
    int end = numbers.size()-1;

    while(start<=end){
      int mid = start + (end-start)/2;
      if(numbers.get(mid) == target) return mid;
      if(numbers.get(mid) < target) start = mid+1;
      if(numbers.get(mid) > target) end = mid-1;
    }
    
    return -1;
  }
```

### 2. binary search index
- return the index where the target can be found within the List.
- If the target is not found in the List, then return the index where it should appear in the sorted order.
  
```
binarySearchIndex(List.of(0, 6, 8, 12, 16, 19, 20, 24, 28), 27); // -> 8
```

```
  public static int binarySearchIndex(List<Integer> nums, int target) {
    int start = 0;
    int end = nums.size()-1;

    while(start<=end){
      int mid = start + (end-start)/2;
      if(nums.get(mid) == target) return mid;
      if(nums.get(mid) < target) start = mid+1;
      if(nums.get(mid) > target) end = mid-1;
    }

    return start;
  }
```

### 3. square root
- Case 1 
<img width="436" height="178" alt="image" src="https://github.com/user-attachments/assets/23d0205f-ff2c-442f-bdaa-3569fe7540da" />.

- Case 2
* Note why we return hi as we want to round to lower value.
<img width="516" height="245" alt="image" src="https://github.com/user-attachments/assets/0ed540d6-c1e1-4a9e-b2fe-248d1cadfda9" />.

```
  public static int squareRoot(int n) {
    int start = 0;
    int end = n;

    while(start<=end){
      int mid = start + (end-start)/2;
      if(mid*mid == n) return mid;
      if(mid*mid < n) start = mid+1;
      if(mid*mid > n) end = mid-1;
    }

    return end;
  }
```

