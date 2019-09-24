# Algorithm 

DP

# Better solution 

Currently Best

# Performance

Runtime: 2 ms, faster than 90.21% of Java online submissions for Minimum Path Sum.

Memory Usage: 42.5 MB, less than 78.38% of Java online submissions for Minimum Path Sum.

# Time spent:

9 min

# Times of Wrong answer:

None

# Solution 

```java
class Solution {
    public int minPathSum(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        
        int[][] sum = new int[grid.length][grid[0].length];
        sum[0][0] = grid[0][0];
        for (int i = 1; i < grid.length; i++) {
            sum[i][0] = sum[i - 1][0] + grid[i][0];
        }
        
        for (int i = 1; i < grid[0].length; i++) {
            sum[0][i] = sum[0][i - 1] + grid[0][i];
        }
        
        for (int i = 1; i < grid.length; i++) {
            for (int j = 1; j < grid[0].length; j++) {
                sum[i][j] = Math.min(sum[i - 1][j], sum[i][j - 1]) + grid[i][j];
            }
        }
        
        return sum[grid.length - 1][grid[0].length - 1];
    }
}
```



# Time complexity

O(n^2)

# Corner cases :

1.  Initialize i == 0 and j == 0 first 

# Notes and Tips