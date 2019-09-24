# Algorithm 

DP

# Better solution 

Currently Best

# Performance

Runtime: 3 ms, faster than 52.97% of Java online submissions for Paint House II.

Memory Usage: 43.1 MB, less than 24.00% of Java online submissions for Paint House II.

# Time spent:

19 min

# Times of Wrong answer:

1- Bug 1

# Solution 

```java
class Solution {
    public int minCostII(int[][] costs) {
        if (costs == null || costs.length == 0 || costs[0].length == 0) {
            return 0;
        }
        //Bug 1 : Corner case, if there is only 1 house, then it is possible to have only one color.
        if (costs[0].length == 1) {
            return costs[0][0];
        }
        
        int k = costs[0].length;
        int[][] paintCost = new int[costs.length + 1][k];
        for (int i = 0; i < k; i++) {
            paintCost[0][i] = 0;
        }
        
        for (int i = 1; i < paintCost.length; i++) {
            int min1 =  Integer.MAX_VALUE, min2 = Integer.MAX_VALUE, index1 = -1, index2 = -1;
            for (int j = 0; j < k; j++) {
                if (paintCost[i - 1][j] < min1) {
                    min2 = min1;
                    index2 = index1;
                    min1 = paintCost[i - 1][j];
                    index1 = j;
                } else if (paintCost[i - 1][j] < min2) {
                    min2 = paintCost[i - 1][j];
                    index2 = j;
                }
            }
            
            for (int j = 0; j < k; j++) {
                if (j != index1) {
                    paintCost[i][j] = min1 + costs[i - 1][j];
                } else {
                    paintCost[i][j] = min2 + costs[i - 1][j];
                }
            }
        }
        
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < k; i++) {
            min = Math.min(min, paintCost[costs.length][i]);
        }
        return min;
    }
}
```



# Time complexity

O(nk)

# Corner cases :

1. If there is only 1 house, then it is possible to have only one color.

# Notes and Tips