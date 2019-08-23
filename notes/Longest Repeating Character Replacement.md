# Algorithm

Two pointers

# Better solution

More concise solution : 

```java
public class Solution {
    public int characterReplacement(String s, int k) {
        int maxLen = 0;
        for(int l = 0 ; l<26;l++){
            char c = (char)('A' + l); //repeated char we are looking for
            int i = 0, j = 0, count = 0;
            while(j<s.length()){
                char cur = s.charAt(j);
                if(cur != c) count++;
                
                //make the substring valid again
                while(count > k){
                    if(s.charAt(i) != c) count--;
                    i++;
                }
                
                //update maximun len
                maxLen = Math.max(maxLen,j-i+1);
                j++;
            }
        }
        return maxLen;
    }
}
```



## Performance:

Runtime: 10 ms, faster than 38.10% of Java online submissions for Longest Repeating Character Replacement.

Memory Usage: 37.2 MB, less than 100.00% of Java online submissions for Longest Repeating Character Replacement.

## Time spent:

50 min 14 seconds 

## Times of Wrong answer:

1- Bug 1

## Solution

```java
class Solution {
    public int characterReplacement(String s, int k) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        
        if (k >= s.length()) {
            return s.length();
        }
        
        int maxLength = 1, start = 0, end = 0, mostFretime = 0;
        int[] map = new int[26];
  
        while (end < s.length()) {
            // NOtation : Try not to use while loop becasue it is easy to write bugs
            map[s.charAt(end) - 'A']++;
            mostFretime = mostFretime < map[s.charAt(end) - 'A'] ? 
                                        map[s.charAt(end) - 'A'] : mostFretime;
            end++;

            // Bug 1 : Be careful with corner case "end = s.length()"
            if (end == s.length() && end - start - mostFretime <= k) {
                maxLength = maxLength < end - start ? end - start : maxLength; 
            }
            
            if (end - start - mostFretime > k) {
                maxLength = maxLength < end - start - 1 ? end - start - 1 : maxLength; 
                map[s.charAt(start) - 'A']--;
                mostFretime = findMostFre(map);
                start++;
            }
        }
        
        return maxLength;
    }
    
    private int findMostFre(int[] map) {
        int max = 0;
        for (int i = 0; i < map.length; i++) {
            max = max < map[i] ? map[i] : max;
        }
        return max;
    }
}
```



# Time complexity

O(nk)

# Notes and Tips

1. Be careful with corner case "end = s.length()"
2. Try not to use while loop becasue it is easy to write bugs