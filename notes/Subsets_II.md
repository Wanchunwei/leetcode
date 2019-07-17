# Algorithm 
DFS(Recursion)

# Better solution 
Currently Best

# Solution 

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();

        /*
         Coding Style Notation: 
         If the given array is null, then directly return null;
        */
        if(nums == null || nums.length == 0){
            return result;
        }

        List<Integer> list = new ArrayList<>();
        int pos = 0;
        
        Arrays.sort(nums);
        
        subsetshelper(result, list, nums, 0);
        
        return result;
    }
    
    void subsetshelper(List<List<Integer>> result,
                       List<Integer> list,
                       int[] nums,
                       int pos){
        result.add(new ArrayList<>(list));
        
        for(int i = pos; i < nums.length; i++){
            if(i != pos && nums[i] == nums[i - 1]){
                continue;
            }
            list.add(nums[i]);
            subsetshelper(result, list, nums, i + 1);
            list.remove(list.size() - 1);
        }
    }
}
```

# Time complexity
T(n) = T(n-1) + T(n-2) + ... +T(0)

O(2＾n)


# Notes and Tips

##  1. Don't delete redundant subsets after searching all subsets. 
The time complexity will be very high in some extreme cases. 

Eg: [1,1,1,1,1,1] 

## 2. Sort list when delete redundant subsets. 
Due to that we don't want redundant subsets, we should use `Arrays.sort()` to sort the given array to gather redundant number. 

## 3. Don't inverse the condition `i != pos && nums[i] == nums[i - 1]`
We must judge `i != pos` and then `nums[i] == nums[i - 1]`, otherwise there will an error.   


# Relavent Question

- [78 Subsets](https://github.com/Wanchunwei/leetcode/blob/master/notes/Subsets.md)


