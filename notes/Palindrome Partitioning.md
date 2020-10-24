# Algorithm 

DFS

# Better solution

Currently Best

## Performance:

Runtime: 2 ms, faster than 97.21% of Java online submissions for Palindrome Partitioning.

Memory Usage: 39.2 MB, less than 97.69% of Java online submissions for Palindrome Partitioning.

## Time spent:

Not Done

## Times of Wrong answer:

None

# Solution 

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> results = new ArrayList<>();
        List<String> temp = new ArrayList<>();
        if (s == null || s.length() == 0) {
            return results;
        }
        boolean[][] palindrome = palin(s);
        
        helper(s, results, temp, 0, palindrome);
        return results;
    }
    
    private void helper(String s, 
                        List<List<String>> results, 
                        List<String> temp, 
                        int startIndex,
                        boolean[][] palindrome) {
        
        if (startIndex == s.length()) {
            results.add(new ArrayList<String>(temp));
        }
        
        for (int i = startIndex; i < s.length(); i++) {
            if (palindrome[startIndex][i]) {
                temp.add(s.substring(startIndex, i + 1));
                helper(s, results, temp, i + 1, palindrome);
                temp.remove(temp.size() - 1);
            }
            
        }
        
        return;
    }
    
    private boolean[][] palin(String s) {
        boolean[][] palindrome = new boolean[s.length()][s.length()];
        for (int i = 0; i < s.length(); i++) {
            palindrome[i][i] = true;
            if (i + 1 < s.length()) {
                palindrome[i][i + 1] = (s.charAt(i) == s.charAt(i + 1));
            }
        }
        
        //Notation : i must start from s.length() - 3 to 0, because palindrome[i + 1][j - 1] must be gone through rather first than palindrome[i][j] 
        for (int i = s.length() - 3; i >= 0; i--) {
            for (int j = i + 2; j < s.length(); j++) {
                palindrome[i][j] = (palindrome[i + 1][j - 1] && s.charAt(i) == s.charAt(j));
            } 
        }
        
        return palindrome;
    }
    
    
}
```

```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        if len(s) == 0:
            return []
        
        results = []
        self.dfs(s, 0, [], results, {})
        return results
    
    # Notation1: Must have index here rather than use the substring of s to replace s. otherwise will cause mistake in isPalindrome function
    def dfs(self, s, index, parti, results, memo):
        if index == len(s):
            results.append(list(parti))
            return 
            
        for i in range(index + 1, len(s) + 1):
            if self.isPalindrome(index, i - 1, memo, s):
                parti.append(s[index:i])
                self.dfs(s, i, parti, results, memo)
                parti.pop()
                
    def isPalindrome(self, start, end, memo, s):
        if (start, end) in memo:
            return memo[(start, end)]
        
        if start == end:
            return True
        
        if start + 1 == end:
            return s[start] == s[end]

        memo[(start, end)] = s[start] == s[end] and self.isPalindrome(start + 1, end - 1, memo, s)
        return memo[(start, end)]
        
```



# Time complexity

O(2^n)

# Note and tips

1. i must start from `s.length() - 3` to `0`, because `palindrome[i + 1][j - 1]` must be gone through first rather than `palindrome[i][j]` 