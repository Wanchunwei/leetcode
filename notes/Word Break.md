# Algorithm 

Dynamic Programming

Analysis : 

1.  Brute force(dfs) with time complexity O(n^N) 
2.  We don't need to print the path, but just answer true/false
3. So, this is a DP problem.

# Better solution 

Currently Best

## Performance:

Runtime: 4 ms, faster than 77.31% of Java online submissions for Word Break.

Memory Usage: 36.3 MB, less than 93.48% of Java online submissions for Word Break.

## Time spent:

None

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> set = new HashSet<>();
        for (String str : wordDict) {
            set.add(str);
        }
        
        boolean[] valid = new boolean[s.length()];
        for (int i = s.length() - 1; i >= 0; i--) {
            if (isValid(i, s, set, valid)) {
                valid[i] = true;
            }
        }
        
        return valid[0];
    }
    
    private boolean isValid(int start, String s, Set<String> set, boolean[] valid) {
        for (int i = start; i < s.length(); i++) {
            if (set.contains(s.substring(start, i + 1)) && (i + 1 == s.length() || valid[i + 1])) {
                return true;
            }
        }
        return false;
    }

}
```

# Time complexity

O(n^2)

# Notes and Tips

