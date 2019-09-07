# Algorithm

Array(Prefix sum)

# Better solution

Currently Best

## Performance:

Total runtime 2987 ms

Your submission beats 65.20% Submissions!

## Time spent:

30 min 

## Times of Wrong answer:

None

## Solution

```java
public class Solution {
    /*
     * @param nums: A list of integers
     * @return: An integer denotes the sum of max two non-overlapping subarrays
     */
    public int maxTwoSubArrays(List<Integer> nums) {
        // write your code here
        if (nums.size() == 1) {
            return nums.get(0);
        }
        
        int[] left = new int[nums.size()];
        int[] right = new int[nums.size()];
        int[] preSum = new int[nums.size() + 1];
        int smallest = preSum[0], curLargetst = Integer.MIN_VALUE;
        
        
        for (int i = 0; i < nums.size(); i++) {
            preSum[i + 1] = preSum[i] + nums.get(i);
            smallest = Math.min(smallest, preSum[i]);
            curLargetst = Math.max(preSum[i + 1] - smallest, curLargetst);
            left[i] = curLargetst;
        }
        
        int largest = preSum[nums.size()], cur = Integer.MIN_VALUE;
        for (int i = nums.size() - 1; i >= 0; i--) {
            largest = Math.max(largest, preSum[i + 1]);
            cur = Math.max(largest - preSum[i], cur);
            right[i] = cur;
            
        }
        
        int largestSum = Integer.MIN_VALUE;
        for (int i = 0; i < nums.size() - 1; i++) {
            largestSum = Math.max(largestSum, left[i] + right[i + 1]);
            
        }
        
        return largestSum;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

