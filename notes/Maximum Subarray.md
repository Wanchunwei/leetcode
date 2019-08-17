# Algorithm

Dynamic Programming

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 87.49% of Java online submissions for Maximum Subarray.

Memory Usage: 41.6 MB, less than 5.16% of Java online submissions for Maximum Subarray.

## Time spent:

5 min 

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        } 
        
        int max = nums[0];
        int[] maxSum = new int[nums.length];
        maxSum[0] = nums[0];
        for (int i = 1; i < nums.length; i++) {
            maxSum[i] = maxSum[i - 1] + nums[i] > nums[i] ? 
                                    maxSum[i - 1] + nums[i] : nums[i];
            max = maxSum[i] > max ? maxSum[i] : max;
        }
        return max;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

