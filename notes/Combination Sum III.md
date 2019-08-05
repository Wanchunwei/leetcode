# Algorithm 

DFS

# Better solution

Currently Best

## Performance:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Combination Sum III.

Memory Usage: 33.7 MB, less than 8.05% of Java online submissions for Combination Sum III.

## Time spent:

7 min 55 seconds

## Times of Wrong answer:

None

# Solution 

```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> results = new ArrayList<>();
        List<Integer> temp = new ArrayList<>();
        if (k == 0 || n <  0) {
            return results;
        }
        
        helper(k, n, results, temp, 1);
        return results;
    }
    
    private void helper(int k, 
                        int remain,
                        List<List<Integer>> results,
                        List<Integer> temp,
                        int startIndex) {
        if (remain == 0 && k == 0) {
            results.add(new ArrayList<Integer>(temp));
            return;
        }
        
        if (remain < 0 || k < 0) {
            return;
        }
        
        for (int i = startIndex; i <= 9; i++) {
            temp.add(i);
            helper(k - 1, remain - i, results, temp, i + 1);
            temp.remove(temp.size() - 1);
        }
    }
}
```

# Time complexity

O(n)

# Note and tips

