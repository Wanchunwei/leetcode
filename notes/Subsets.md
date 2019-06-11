# Solution 

Runtime: 0 ms, faster than 100.00% of Java online submissions for Subsets.

Memory Usage: 37.3 MB, less than 98.76% of Java online submissions for Subsets.

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<Integer> list = new ArrayList<>();
        List<List<Integer>> result = new ArrayList<>();
        
        subsethelper(result, list, nums, 0);
        
        return result;
    }
    
    public void subsethelper(List<List<Integer>> result,
                     List<Integer> list,
                     int[] nums,
                     int pos){
        result.add(new ArrayList<>(list));
        
        for(int i = pos; i < nums.length; i++){
            list.add(nums[i]);
            subsethelper(result, list, nums, i + 1);
            list.remove(list.size() - 1);
        }
    }
}
```

# Algorism 
1. DFS(Recursion)

# Time complexity


# Better solution 
Currently Best

# Notes

# Relavent Question
- [90 Subsets II](https://github.com/Wanchunwei/leetcode/blob/master/notes/SubsetsII.md)

