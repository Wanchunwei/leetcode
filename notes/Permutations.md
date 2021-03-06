# Algorithm 

DFS

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 98.44% of Java online submissions for Permutations.

Memory Usage: 36.5 MB, less than 96.66% of Java online submissions for Permutations.

## Time spent:

6 min 48 seconds

## Times of Wrong answer:

None

# Solution 

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> results = new ArrayList<>();
        List<Integer> temp = new ArrayList<>();
        if (nums == null) {
            return results;
        }          
                  
        if (nums.length == 0) {
            results.add(temp);
            return results;
        }
        
        boolean[] visited = new boolean[nums.length];
        helper(nums, results, temp, visited);
        return results;
    }
                  
    private void helper(int[] nums, 
                        List<List<Integer>> results, 
                        List<Integer> temp,
                        boolean[] visited) {
        if (temp.size() == nums.length) {
            results.add(new ArrayList<Integer>(temp));
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (!visited[i]) {
                temp.add(nums[i]);
                visited[i] = true;
                helper(nums, results, temp, visited);
                visited[i] = false;
                temp.remove(temp.size() - 1);
            }
        }
    }
}
```

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        if not nums:
            return [[]]
        
        results = []
        self.dfs(nums, [], set(), results)
        return results
    
    def dfs(self, nums, perm, container, results):
        if (len(nums) == len(perm)):
            results.append(list(perm))
            return 
        
        for i in range(0, len(nums)):
            if nums[i] not in container:
                perm.append(nums[i])
                container.add(nums[i])
                self.dfs(nums, perm, container, results)
                container.remove(nums[i])
                perm.pop()
```



# Time complexity

O(n)

# Note and tips

