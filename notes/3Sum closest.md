# Algorithm

Two pointers

# Better solution

Currently Best

## Performance:

Runtime: 5 ms, faster than 63.02% of Java online submissions for 3Sum Closest.

Memory Usage: 36.6 MB, less than 100.00% of Java online submissions for 3Sum Closest.

## Time spent:

Not Done

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        int min = Integer.MAX_VALUE;
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
           if (Math.abs(twoSum(nums, i + 1, target - nums[i])) == 0) {
               return target;
           }
            
           if (Math.abs(twoSum(nums, i + 1, target - nums[i])) <= Math.abs(min)) {
               min = twoSum(nums, i + 1, target - nums[i]);
           }
        }
        return min + target;
    }
    
    private int twoSum(int[] nums, int sta, int target) {
        int start = sta, end = nums.length - 1, min = Integer.MAX_VALUE;
        while (start < end) {
            if (start < end && nums[start] + nums[end] > target) {
                min = Math.abs(min) > Math.abs(nums[start] + nums[end] - target) ? 
                    (nums[start] + nums[end] - target) : min;
                end--;
            } else if (start < end && (nums[start] + nums[end] == target)) {
                return 0;
            } else if (start < end && nums[start] + nums[end] < target) {
                min = Math.abs(min) > Math.abs(nums[start] + nums[end] - target) ? 
                    (nums[start] + nums[end] - target) : min;
                start++;
            }
            
            if (start < end) {
                    min = Math.abs(min) > Math.abs(nums[start] + nums[end] - target) ? 
                                                  (nums[start] + nums[end] - target) : min;
            }                    
        }
        return min;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

