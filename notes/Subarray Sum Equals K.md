# Algorithm 

Linked List and Array(Prefix Sum)

# Better solution

Currently Best

## Performance:

Total runtime 517 ms

Your submission beats 46.00% Submissions!

## Time spent:

20 min

## Times of Wrong answer:

2 - Bug 1, Bug 2

# Solution 

```java
public class Solution {
    /**
     * @param nums: a list of integer
     * @param k: an integer
     * @return: return an integer, denote the number of continuous subarrays whose sum equals to k
     */
    public int subarraySumEqualsK(int[] nums, int k) {
        // write your code here
        int count = 0;
        if (nums == null || nums.length == 0){
            return count;
        }
        
        Map<Integer, Integer> map = new HashMap<>();
        int[] preSum = new int[nums.length + 1];
        //Bug 1 : Rmember to add preSum[0] to map
        map.put(preSum[0], 1);
        for (int i = 0; i < nums.length; i++) {
            preSum[i + 1] = preSum[i] + nums[i];
            if (!map.containsKey(preSum[i + 1])) {
                map.put(preSum[i + 1], 1);
            } else {
                //Bug 2 : We must count number of map.get(preSum[i + 1])
                map.put(preSum[i + 1], map.get(preSum[i + 1]) + 1);
            }
            
            if (map.containsKey(preSum[i + 1] - k)) {
                count += map.get(preSum[i + 1] - k);
            }
            
        }
        
        return count;
    }
}
```

# Time complexity

O(n)

# Note and tips

1. Rmember to add preSum[0] to map
2. We must count number of map.get(preSum[i + 1])