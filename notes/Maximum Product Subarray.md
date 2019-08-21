# Algorithm

Dynamic Programming

# Better solution

Currently Best

## Performance:

Runtime: 2 ms, faster than 52.49% of Java online submissions for Maximum Product Subarray.

Memory Usage: 37.8 MB, less than 13.42% of Java online submissions for Maximum Product Subarray.

## Time spent:

5 min 

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    public int maxProduct(int[] nums) {
        long max = nums[0];
        long[] maxProduct = new long[nums.length];
        long[] minProduct = new long[nums.length];
        maxProduct[0] = nums[0];
        minProduct[0] = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] < 0) {
                maxProduct[i] = Math.max(nums[i], nums[i]*minProduct[i - 1]);
                minProduct[i] = Math.min(nums[i], nums[i]*maxProduct[i - 1]);
            }
            
            if (nums[i] > 0) {
                maxProduct[i] = Math.max(nums[i], nums[i]*maxProduct[i - 1]);
                minProduct[i] = Math.min(nums[i], nums[i]*minProduct[i - 1]);
            }
            
            if (nums[i] == 0) {
                maxProduct[i] = 0;
                minProduct[i] = 0;
            }
            
            max = max < maxProduct[i] ? maxProduct[i] : max;
            
        }
        return (int)max;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

