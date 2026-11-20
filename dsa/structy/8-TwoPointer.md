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
```
