### 1. is palindrome

<img width="550" height="297" alt="image" src="https://github.com/user-attachments/assets/8244975b-8828-4ba5-a140-31f823499020" />


```
isPalindrome("pop") // -> true
isPalindrome("pops") // -> false
```
```
public static boolean isPalindrome(String s) {
    int start = 0;
    int end = s.length()-1;

    while(start<=end){
      if(s.charAt(start) != s.charAt(end)) return false;
      start++;
      end--;
    }
    
    return true;
  }
// Time: O(n)
// Space: O(1)
```

### 2. uncompress

```Source.uncompress("3n12e2z"); // -> "nnneeeeeeeeeeeezz"```

```
  public static String uncompress(String s) {
    StringBuilder uncompressedString =  new StringBuilder();
    StringBuilder digits = new StringBuilder();
    int start = 0;
    int end = 0;
   
    while(end<s.length()){
      char endChar = s.charAt(end);
      if(Character.isDigit(endChar)){
        digits.append(endChar);
      }else{
        int multiples = Integer.parseInt(digits.toString()); 
        for(int i=0; i<multiples; i++){
          uncompressedString.append(String.valueOf(endChar));
        }
        digits = new StringBuilder();
      }
      end++;
      start = end;
    }
    return uncompressedString.toString();
  }
// n = number of groups
// m = max num found in any group
// Time: O(n*m)
// Space: O(n*m)
```

### 3. compress
```
'aaa' compresses to '3a'
'cc' compresses to '2c'
't' should remain as 't'

Source.compress("ccaaatsss"); // -> "2c3at3s"
```

<img width="519" height="354" alt="image" src="https://github.com/user-attachments/assets/a9d8fa8c-d4eb-4d9c-a5bc-ce182d21f282" />. 

```
  public static String compress(String s) {
    int start = 0;
    int end = 0;
    Character c = s.charAt(0);
    StringBuilder result = new StringBuilder();
    int num = 0;
    
    while(end<s.length()){
      Character endChar = s.charAt(end);
      if(c != endChar){
          num = end-start;
        if(num>1 ) result.append(String.valueOf(num));
        result.append(String.valueOf(c));
        start = end;
        c = endChar;
      }
      end++;
    }

    num = end-start;
    if(num>1 ) result.append(String.valueOf(num));
    result.append(String.valueOf(c));
    
    return result.toString();
  }
// Time: O(n)
// Space: O(n)
```

### 4. five sort
IMP: Need to update the array in place.

```
List<Integer> array = new ArrayList<>(List.of(12, 5, 1, 5, 12, 7));
Source.fiveSort(array);
// -> [12, 7, 1, 12, 5, 5] 
```

```
  public static List<Integer> fiveSort(List<Integer> array) {
    int start =0;
    int end =array.size()-1;

    while(start<end){
      while(array.get(end) == 5) end--;
      if(array.get(start) == 5){
        array.set(start,array.get(end));
        array.set(end,5);
        end--;
      }
      start++;
    }
    return array;
  }
// Time: O(n)
// Space: O(1)
```

### 5. is subsequence

```
isSubsequence("bde", "abcdef"); // -> true
isSubsequence("bda", "abcdef"); // -> false
```

```
  public static boolean isSubsequence(String string1, String string2) {
    int i1 = 0;
    int i2 = 0;

    while(i1<string1.length() && i2<string2.length()){
      if(string1.charAt(i1) == string2.charAt(i2)){
        i1++;
        i2++;
      }else{
        i2++;
      }
    }

    if(i1 == string1.length()) return true;
    return false;
  }
// n = length of string1
// m = length of string2
// Time: O(m)
// Space: O(1)
```
