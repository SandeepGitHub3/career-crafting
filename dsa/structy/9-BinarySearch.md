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

### 4. find leftmost index

<img width="597" height="248" alt="image" src="https://github.com/user-attachments/assets/7acdc243-b49f-4123-8490-f2613f0131da" />

```
  public static int findLeftmostIndex(List<Integer> nums, int target) {
    int start = 0;
    int end = nums.size()-1;
    int result = -1;

    while(start<=end){
      int mid = start+(end-start)/2;
      int midEle = nums.get(mid);
      if(midEle > target) end = mid - 1;
      if(midEle < target) start = mid + 1;
      if(midEle == target){
        result = mid; // remember it
        end = mid-1; // but keep looking left
      }
    }
    return result;
  }
```

### 5. count in sorted array

```countInSortedArray(List.of(1,2,3,3,3,3,3,4,5,6,6,7,8,8,8,9), 3); // -> 5```. 

<img width="679" height="385" alt="image" src="https://github.com/user-attachments/assets/6a5a8384-039c-421c-ab5b-a33f9ea8df91" />. 

```
public static int countInSortedArray(List<Integer> nums, int target) {
    int leftMostIndex = findLeftMostIndex(nums,target);
    if (leftMostIndex == -1) return 0;
    int rightMostIndex = findRightMostIndex(nums,target);
    return rightMostIndex-leftMostIndex +1;
  }

  private static int findLeftMostIndex(List<Integer> nums, int target){
    int start = 0;
    int end = nums.size()-1;
    int index = -1;

    while(start<=end){
      int mid = start+(end-start)/2;
      int midEle = nums.get(mid);
      if(midEle > target) end = mid - 1;
      if(midEle < target) start = mid + 1;
      if(midEle == target){
        index = mid;
        end = mid-1; //keep looking left
      }
    }
    return index;
  }

  private static int findRightMostIndex(List<Integer> nums, int target){
    int start = 0;
    int end = nums.size()-1;
    int index = -1;

    while(start<=end){
      int mid = start+(end-start)/2;
      int midEle = nums.get(mid);
      if(midEle > target) end = mid - 1;
      if(midEle < target) start = mid + 1;
      if(midEle == target){
        index = mid;
        start = mid+1; // keep looking right
      }
    }
    return index;
  }
```

### 6. min in rotated sorted array - Difficult : 🔴

```
minInRotatedSortedArray(List.of(6,7,9,10,2,3,4,5)); // -> 2
// the original array was [2,3,4,5,6,7,9,10] and was rotated 4 times
```

<img width="726" height="351" alt="image" src="https://github.com/user-attachments/assets/48e304b4-c51c-470d-889f-d41bf074e84d" />. 
<img width="680" height="303" alt="image" src="https://github.com/user-attachments/assets/fed984bd-8e3e-4ac3-8842-a43f2255bd37" />. 

```
  public static int minInRotatedSortedArray(List<Integer> nums) {
    int start = 0 ;
    int end = nums.size()-1;

    while(start<end){
      int mid = start + (end-start)/2;
      if(nums.get(mid)<nums.get(end)) 
        end = mid;
      else
        start = mid+1;
    }
    
    return nums.get(start);
  }
```

### 7. find in rotated sorted array - Difficult : 🔴
```
findInRotatedSortedArray(List.of(5,6,7,9,2,3,4), 7); // -> 2
// the original array was [2,3,4,5,6,7,9] and was rotated 4 times
```

- Find the inflection Point and then split the Original Array into 2 sorted arrays.
- Then Do binary search on both the arrays.

<img width="622" height="317" alt="image" src="https://github.com/user-attachments/assets/c142d2d4-d0b7-4050-a346-68b5738d2d2f" />. 

```
public static int findInRotatedSortedArray(List<Integer> nums, int target) {
    int inflectionPoint = findMinIndex(nums);
    int leftResult = binarySearch(nums,target,0,inflectionPoint-1);
    int rightResult = binarySearch(nums,target,inflectionPoint,nums.size()-1);
    if (leftResult == -1) {
      return rightResult;
    } else {
      return leftResult;
    }
  }

  private static int binarySearch(List<Integer> nums, int target, int start, int end){
    while(start<=end){
      int mid = start + (end-start)/2;
      if(nums.get(mid) == target) return mid;
      if(nums.get(mid) > target) 
        end = mid-1;
      else 
        start = mid+1;
    }

    return -1;
  }
  private static int findMinIndex(List<Integer> nums) {
    int start = 0 ;
    int end = nums.size()-1;

    while(start<end){
      int mid = start + (end-start)/2;
      if(nums.get(mid)<nums.get(end)) 
        end = mid;
      else
        start = mid+1;
    }
    
    return start;
  }
```

### 8 . find peak : Difficult 🔴
- return the index of a "peak" element. A "peak" is an element that is greater than both of its adjacent neighbors.
- first and last elements of the List only need to be greater than their single neighbor to be considered a "peak".
- solution should have a time complexity of O(logn).

<img width="704" height="342" alt="image" src="https://github.com/user-attachments/assets/c4470f16-0cff-43f7-a0e8-45cc824ecc32" />. 
<img width="670" height="215" alt="image" src="https://github.com/user-attachments/assets/b44d75b9-eb83-4972-8b1d-929ec6e699e7" />. 
<img width="328" height="252" alt="image" src="https://github.com/user-attachments/assets/08e32dec-a963-426f-8950-0e5ac426da76" />

```
  public static int findPeak(List<Integer> nums) {
    int lo = 0;
    int hi = nums.size() - 1;
    while (lo < hi) {
      int mid = (lo + hi) / 2;
      if (nums.get(mid) < nums.get(mid + 1)) {
        lo = mid + 1;
      } else {
        hi = mid;
      }
    }
    return lo;
  }
```
  

