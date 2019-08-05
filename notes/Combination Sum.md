# Algorithm 

DFS

# Better solution

Currently Best

## Performance:

Runtime: 5 ms, faster than 47.08% of Java online submissions for Combination Sum.

Memory Usage: 38.1 MB, less than 99.06% of Java online submissions for Combination Sum.

## Time spent:

21 min 40 seconds

## Times of Wrong answer:

None

# Solution 

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> results = new ArrayList<>();
        List<Integer> temp = new ArrayList<>();
        if (candidates == null) {
            return results;
        }
        
        Arrays.sort(candidates);
        helper(candidates, target, results, temp, 0);
        return results;
    }
    
    private void helper(int [] candidates,
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
            if (i > startIndex && candidates[i] == candidates[i - 1]) {
                continue;
            }
            
            temp.add(candidates[i]);
            helper(candidates, remainTarget - candidates[i], results, temp, i);
            //Notation : Remember to remove `candidates[i]`  for next loop after adding it.
            temp.remove(temp.size() - 1);
        }
    }
}
```

# Time complexity

O(n)

# Note and tips

1. Remember to remove `candidates[i]`  for next loop after adding it.