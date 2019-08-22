# Algorithm

Two pointers

# Better solution

Currently Best

## Performance:

Runtime: 10 ms, faster than 43.41% of Java online submissions for Find K-Length Substrings With No Repeated Characters.

Memory Usage: 36.4 MB, less than 100.00% of Java online submissions for Find K-Length Substrings With No Repeated Characters.

## Time spent:

5 min 

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    public int numKLenSubstrNoRepeats(String S, int K) {
        if (K > S.length()) {
            return 0;
        }
        
        Set<Character> set = new HashSet<>();
        int start = 0, end = 0, count = 0;
        while (end < S.length()) {
            while (end < S.length() && (end - start + 1) <= K && !set.contains(S.charAt(end))) {
                set.add(S.charAt(end));
                end++;
            }
            
            if (set.size() == K) {
                count++;
            }
            
            set.remove(S.charAt(start));
            start++;
        }
        return count;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

