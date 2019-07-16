# Algorithm 

Binary Search

Analysis: Binary search for answer

1. Find start point and end point which are the minimum and maximum in the given array.
2.  do while loop until `start + 1e-5 < end` 
3. Find whether there exists a Subarray (length >= k) whose average >= `mid`  
   - Translate nums[0] + nums[1] + ... + nums[i] >= average * k to (nums[0] - average) + (nums[1] - average) + ... + (nums[n] - average) >= 0 
   - Traverse the given array, set the sum = the cumulative sum from 0 to i and the preSum = the min value of all the cumulative sum from 0 to all the index before i - k. 
   - Then `sum - preSum` means the maximum average value of all the Subarray length >= k) whose end point is i. So  if `sum - preSum >= 0`  return true.

# Better solution 

Currently Best

## Performance:

Runtime: 25 ms, faster than 69.62% of Java online submissions for Maximum Average Subarray II.

Memory Usage: 40.4 MB, less than 88.89% of Java online submissions for Maximum Average Subarray II.

## Time spent:

19  min 16 seconds

## Times of Wrong answer:

1 - Bug 1

## Solution

```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        double start = 10000, end = -10000;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] < start) {
                start = nums[i];
            }
            
            if (nums[i] > end) {
                end = nums[i];
            }
        }
        
        while (start + 1e-5 < end) {
            double mid = start + (end - start) / 2;
            if (exist(mid, nums, k)) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        return start;
    }
    
    private boolean exist(double average, int[] nums, int k) {
        double sum = 0, preSum = 0, minPreSum = 0;
        for (int i = 0; i < nums.length; i++) {
            if (i < k) {
                sum += nums[i] - average;
            } else {
                if (sum >= minPreSum) {
                    return true;
                }
                sum += nums[i] - average;
                // Bug 1: Remember to minus average when adding to preSum
                preSum += nums[i - k] -average;
                minPreSum = Math.min(preSum, minPreSum);
            }
        }
        
        if (sum >= minPreSum) {
            return true;
        }
        
        return false;
    }
}
```

# Time complexity

O(nlog(max - min))

# Notes and Tips

1. When calculating average, Converting nums[0] + nums[1] + ... + nums[i] >= average * k to (nums[0] - average) + (nums[1] - average) + ... + (nums[n] - average) >= 0 is a common way to simplify problem. 
2. MaxSum(Subarray with length >= K) = MaxSum (Sum(Subarray with length i) - MinSum(Subarray with length i - k))