Intro:
<img width="662" height="310" alt="image" src="https://github.com/user-attachments/assets/36fa380b-6295-4a7f-955a-bfd4d7e5d3b2" />


1.max subarray sum size k
Write a method that takes in a List of numbers and a size k as arguments. The method should return the maximum sum of subarrays that contain exactly k elements.

You can assume that k is less than or equal to the length of the input List.


Brute force:
Consider every combination of subarrays.
TIme complexity is O(n2)


public static int maxSubarraySumSizeK(List<Integer> nums, int k) {
    int currSum = 0;
    for(int i=0; i<k; i++){
      currSum = currSum+ nums.get(i);
    }

    
    int maxSum = currSum;
//i<nums.size()-k - conould be confusing check
//try to dry run for cases like maxSubarraySumSizeK(List.of(2, 1, 5) , 3); 
    for(int i=0; i<nums.size()-k; i++){
      currSum = currSum - nums.get(i);
      currSum = currSum + nums.get(i+k);
      maxSum = Math.max(maxSum,currSum);
    }
    
    return maxSum;
  }


  mention time and space complxity

  2.max subarray product size k
Write a method that takes in a List of numbers and a size k as arguments. The method should return the maximum product of subarrays that contain exactly k elements.

You can assume that k is less than or equal to the length of the input List.

You can assume that numbers of the List are non-zero.


 public static double maxSubarrayProductSizeK(List<Double> nums, int k) {
    Double currProduct = nums.get(0);
    for(int i =1 ; i<k ; i++){
      currProduct = currProduct * nums.get(i); 
    }

    Double maxProduct = currProduct;

    for(int i = 0; i<nums.size()-k; i++){
      currProduct = currProduct/nums.get(i);
      currProduct = currProduct * nums.get(i+k);
      maxProduct = Math.max(maxProduct,currProduct);
    }
    
    return maxProduct;
  }


3. subarray target sum size k
Write a method that takes in a List of numbers, a target sum, and a size k as arguments. The method should return the number of subarrays of size k that sum to the target.

You can assume that k is less than or equal to the length of the input List.

public static int subarrayTargetSumSizeK(List<Integer> nums, int target, int k) {
    int sum = 0;
    int targetSumCount = 0;
    for(int i=0; i<k; i++){
      sum = sum+nums.get(i);
    }

    if(sum == target)
      targetSumCount++;   

    for(int i=0; i<nums.size()-k; i++){
        sum = sum-nums.get(i);
        sum = sum+nums.get(i+k);
        if(sum == target)
          targetSumCount++;
    }
    
    return targetSumCount;
  }

  4.has substring anagram
Write a function that takes in a string and an anagram. The function should return a boolean indicating whether or not the string contains a substring with the same characters as the anagram.

You can assume that the string contains no duplicate characters.

You can assume that the anagram contains no duplicate characters.

You can assume that the anagram is not longer than the string.

public static boolean hasSubstringAnagram(String s, String anagram) {
    Set<Character> anagramSet = new HashSet<>();
    for(char c: anagram.toCharArray()){
      anagramSet.add(c);
    }

    Set<Character> windowSet = new HashSet<>();
    for(int i=0; i<anagram.length(); i++){
      windowSet.add(s.charAt(i));
    }

    if(windowSet.equals(anagramSet)) return true;

    for(int i=0; i< s.length()-anagram.length(); i++){
      windowSet.remove(s.charAt(i));
      windowSet.add(s.charAt(i+anagram.length()));
      if(windowSet.equals(anagramSet)) return true;
    }
    return false;
  }

  5.count substring anagrams
Write a method that takes in a string and an anagram. The method should return the number of substrings that appear in the string that have the same characters as the anagram.

You can assume that the anagram is not longer than the string.
// imp- check there could be dupes here and hence we need a map.


public static int countSubstringAnagrams(String s, String anagram) {
    if (s.length() == 0 || anagram.length() == 0) return 0;

    int k = anagram.length();
    HashMap<Character, Integer> anagramMap = new HashMap<>();
    HashMap<Character, Integer> windowMap = new HashMap<>();

    for (int i = 0; i < k; i++) {
        char aChar = anagram.charAt(i);
        char sChar = s.charAt(i);
        anagramMap.put(aChar, anagramMap.getOrDefault(aChar, 0) + 1);
        windowMap.put(sChar, windowMap.getOrDefault(sChar, 0) + 1);
    }

    int count = anagramMap.equals(windowMap) ? 1 : 0;

    for (int i = 0; i < s.length() - k; i++) {
        char remove = s.charAt(i);
        char add = s.charAt(i + k);

        // Shrink left
        int removeCount = windowMap.get(remove) - 1;
        if (removeCount == 0) windowMap.remove(remove);
        else windowMap.put(remove, removeCount);

        // Expand right
        windowMap.put(add, windowMap.getOrDefault(add, 0) + 1);

        if (anagramMap.equals(windowMap)) count++;
    }

    return count;
}
