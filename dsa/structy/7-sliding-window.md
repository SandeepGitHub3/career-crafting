# Intro:  

<img width="662" height="310" alt="image" src="https://github.com/user-attachments/assets/36fa380b-6295-4a7f-955a-bfd4d7e5d3b2" />


## 1.max subarray sum size k. 

```
maxSubarraySumSizeK(List.of(4, 2, 1, -9, 8, 4, 3), 3); // -> 15
// [8,4,3] is the subarray of size 3 with the maximal sum
```

Brute force:
Consider every combination of subarrays.
Time complexity is O(nk)

<img width="404" height="289" alt="image" src="https://github.com/user-attachments/assets/ad4244d4-a43b-4450-b32d-c13deddc5dda" />. 


<img width="563" height="325" alt="image" src="https://github.com/user-attachments/assets/653e1db8-09ce-4318-bef8-ea05b21ac24e" />

```
public static int maxSubarraySumSizeK(List<Integer> nums, int k) {
   int currSum = 0;

    for(int i=0; i < k; i++){
      currSum = currSum+nums.get(i);
    }

    int maxSum = currSum;

     //i<nums.size()-k - conould be confusing check
    //(4, 2, 1, -9, 8, 4, 3) --> 8,4,3 is the last window we need to go to..so i<=4 --> 7-3 = 4
    for (int i = 0; i < nums.size() - k; i++) {
      currSum = currSum - nums.get(i) + nums.get(i + k);
      maxSum = Math.max(maxSum, currSum);
    }
    
    return maxSum;
}
```

## 2. max subarray product size k

```
maxSubarrayProductSizeK(List.of(4., 2., 1., -9., 8., 2., 3.), 3); // -> 48
// [8,2,3] is the subarray of size 3 with the maximal product
```

```
  public static double maxSubarrayProductSizeK(List<Double> nums, int k) {
    Double currProduct = nums.get(0);

    for(int i=1; i < k; i++){
      currProduct = currProduct * nums.get(i);
    }

    Double maxProduct = currProduct;

    for(int i=0 ; i< nums.size()-k; i++){
      currProduct = currProduct/nums.get(i);
      currProduct = currProduct* nums.get(i+k);
      maxProduct = Math.max(maxProduct,currProduct);
    }
    
    return maxProduct;
  }
```

## 4.has substring anagram

```
hasSubstringAnagram("greyhounds", "hoy"); // -> true
// the substring "yho" is an anagram of "hoy"
```

```
  public static boolean hasSubstringAnagram(String s, String anagram) {
    Set<Character> anagramSet = new HashSet<>();
    for (char c : anagram.toCharArray()) {
      anagramSet.add(c);
    }
    
    int windowSize = anagramSet.size();

    int currMatchCount = 0;
    for(int i =0 ; i<windowSize; i++){
      if(anagramSet.contains(s.charAt(i))) 
        currMatchCount++;
    }

    if (currMatchCount == windowSize) return true;

     for(int i =0 ; i<s.length() - windowSize; i++){
       if(anagramSet.contains(s.charAt(i))) currMatchCount--;
       if(anagramSet.contains(s.charAt(i+windowSize))) currMatchCount++;
       if(currMatchCount == windowSize) return true;
     }
    
    return false;
  }
// n = length of string
// k = length of anagram
// Time: O(n*k)
// Space: O(k)
```


## 5.count substring anagrams

```
countSubstringAnagrams("tacoctacabcatt", "cat"); // -> 4
// the 4 substrings that are an anagram of "cat" are:
//  - tac
//  - cta
//  - tac
//  - cat
```
* imp- check there could be dupes here and hence we need a map.
  
```
  public static int countSubstringAnagrams(String s, String anagram) {
    HashMap<Character,Integer> anagramMap = new HashMap<>();
    for (char c : anagram.toCharArray()) {
      if(!anagramMap.containsKey(c)) anagramMap.put(c,0);
      anagramMap.put(c,anagramMap.get(c)+1);
    }

    int windowSize = anagram.length();

    HashMap<Character,Integer> windowMap = new HashMap<>();
    int anagramCount =  0;
    
    for(int i =0 ; i<windowSize; i++){
      if(anagramMap.containsKey(s.charAt(i))){
        windowMap.put(s.charAt(i),windowMap.getOrDefault(s.charAt(i),0)+1);
      }
    }

    if (windowMap.equals(anagramMap)) anagramCount++;

    for(int i =0 ; i<s.length() - windowSize; i++){
       if(anagramMap.containsKey(s.charAt(i))) {
         windowMap.put(s.charAt(i),windowMap.getOrDefault(s.charAt(i),0)-1);
       }
      
       if(anagramMap.containsKey(s.charAt(i+windowSize))) {
         windowMap.put(s.charAt(i+windowSize),windowMap.getOrDefault(s.charAt(i+windowSize),0)+1);
       }
      
       if (windowMap.equals(anagramMap)) anagramCount++;
     }
    
    return anagramCount;
  }
// n = length of string
// k = length of anagram
// Time: O(n*k)
// Space: O(k)
```
## Sliding Window with Variiable Size

<img width="614" height="420" alt="image" src="https://github.com/user-attachments/assets/e64721bc-5adf-46ed-93fc-df96be782ec4" />

### 6. find subarray sum

<img width="612" height="236" alt="image" src="https://github.com/user-attachments/assets/f80461fb-e352-4309-8ed1-453260d7d491" />. 

```
findSubarraySum(List.of(1, 2, 3, 7, 5), 12); // -> [1,3]
// the subarray that spans indices 1 to 3 is [2,3,7] and its sum is 12
```

```
 public static List<Integer> findSubarraySum(List<Integer> nums, int targetSum) {
    int windowSum = 0;
    int start = 0;
    for (int end = 0; end < nums.size(); end += 1) {
      windowSum += nums.get(end);
      while (windowSum > targetSum) {
        windowSum -= nums.get(start);
        start += 1;
      }

      if (windowSum == targetSum) {
        return List.of(start, end);
      }
    }
    return null;
  }
```
### 7. longest subarray sum

<img width="425" height="229" alt="image" src="https://github.com/user-attachments/assets/1f3e9077-8263-48cd-a4ea-ca88a2c3db67" />

```
longestSubarraySum(List.of(1, 2, 1, 5, 2, 3, 10, 1, 9, 4, 3, 3, 7), 10); // -> 4
// the longest subarray with a sum of 10 is [2, 1, 5, 2] and its length is 4
```

```
  public static int longestSubarraySum(List<Integer> nums, int targetSum) {
    int windowSum = 0;
    int maxWindowSize = -1;
    int start = 0;
    int end = 0;

    while(end<nums.size()){
      windowSum = windowSum + nums.get(end);

      while(windowSum>targetSum){
        windowSum = windowSum - nums.get(start);
        start++;
      }

      if(windowSum == targetSum){
        maxWindowSize = Math.max(maxWindowSize,end-start+1);
      }

      end++;
    }
    return maxWindowSize;
  }
// n = length of list
// Time: O(n)
// Space: O(1)
```
