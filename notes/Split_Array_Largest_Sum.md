# Algorithm 

Binary Search 

Analysis : (Binary Search Answer)

# Better solution 

Currently Best

# Solution 

## Time spent: 

19 min 23 seconds

# Times of wrong answer:

4 - Bug 1, 2, 3,4

```java
class Solution {
    public int splitArray(int[] nums, int m) {
        //Bug 3 : Notice that end is the sum of a integer array, so end should be long             but not int
        long start = nums[0], end = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] < start) {
                start = nums[i];
            }
            end += nums[i];
        }
        
        while (start + 1 < end) {
            long mid = start + (end - start) / 2;
            //Bug 4: If can Split into less than m subarrays, then the mid should be                   smaller
            if (canSplit(mid, nums, m)) {
                end = mid;
            } else {
                start = mid;
            }
        }
 
        if (canSplit(start, nums, m)) {
            return (int)start;
        }
        
        return (int)end;
    }
    
    private boolean canSplit(long minSum, int[] nums, int m) {
        long tempSum = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > minSum) {
                return false;
            }
            
            tempSum += nums[i];
            if (tempSum > minSum) {
                m--;
                tempSum = 0;
                i--;
            } else if (tempSum == minSum) {
                m--;
                tempSum = 0;
            }
            //Bug 1, 2: Notice tempSum < minSum && tempSum != 0
            //Notation 1: if the condition can not cover the last element, we can write                 it after for loop
            if (i == nums.length - 1 && tempSum < minSum && tempSum != 0) {
                m--;
            }
        }
        
        if (m < 0) {
            return false;
        }
        
        return true;
    }
}
```

# Time complexity

O(nlogn)

# Notes and Tips

1. if the condition can not cover the last element, the condition can be written again after for loop. (Here refer to Copy Book)

