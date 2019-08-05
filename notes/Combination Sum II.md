# Algorithm 

DFS

# Better solution

Currently Best

## Performance:

Runtime: 6 ms, faster than 47.84% of Java online submissions for Combination Sum II.

Memory Usage: 37.9 MB, less than 88.55% of Java online submissions for Combination Sum II.

## Time spent:

9 min 40 seconds

## Times of Wrong answer:

None

# Solution 

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> results = new ArrayList<>();
        List<Integer> temp = new ArrayList<>();
        if (candidates == null || candidates.length == 0) {
            return results;
        }
        
        Arrays.sort(candidates);
        helper(candidates, target, results, temp, 0);
        return results;
    }
    
    private void helper(int[] candidates,
                        int remainTarget,
                        List<List<Integer>> results,
                        List<Integer> temp,
                        int startIndex) {
        if (remainTarget == 0) {
            results.add(new ArrayList<Integer>(temp));
            return;
        }
        
        if (remainTarget < 0) {
            return;
        }
        
        for (int i = startIndex; i < candidates.length; i++) {
            if (i != startIndex && candidates[i] == candidates[i - 1]) {
                continue;
            }
            
            temp.add(candidates[i]);
            helper(candidates, remainTarget - candidates[i], results, temp, i + 1);
            temp.remove(temp.size() - 1);
        }
    }
}
```

# Time complexity

O(n)

# Note and tips

