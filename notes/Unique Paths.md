# Algorithm 

DP

# Better solution 

Currently Best

# Performance

Runtime: 0 ms, faster than 100.00% of Java online submissions for Unique Paths II.

Memory Usage: 38.4 MB, less than 96.92% of Java online submissions for Unique Paths II.

# Time spent:

15 min

# Times of Wrong answer:

1 - Bug 1

# Solution 

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid == null || obstacleGrid.length == 0 || obstacleGrid[0].length == 0) {
            return 0;
        }
        
        int[][] paths = new int[obstacleGrid.length][obstacleGrid[0].length];
        //Bug 1 : Corner case, if (i == 0 || j == 0) && obstacleGrid[i][j] == 1, then we need to break because following position will all be 0;
        for (int i = 0; i < obstacleGrid.length; i++) {
            if (obstacleGrid[i][0] != 1) {
                paths[i][0] = 1;
            } else {
                break;
            }
        }
        
        for (int i = 0; i < obstacleGrid[0].length; i++) {
            if (obstacleGrid[0][i] != 1) {
                paths[0][i] = 1;
            } else {
                break;
            }
        }
        
        for (int i = 1; i < obstacleGrid.length; i++) {
            for (int j = 1; j < obstacleGrid[0].length; j++) {
                if (obstacleGrid[i][j] == 1) {
                    paths[i][j] = 0;
                } else {
                    paths[i][j] = paths[i][j - 1] + paths[i - 1][j];
                }
            }
        }
        
        return paths[obstacleGrid.length - 1][obstacleGrid[0].length - 1];
    }
}
```



# Time complexity

O(n^2)

# Corner cases :

1. When i == 0 or j == 0:

   - if obstacleGrid[i] [j] == 0 then paths[i] [j] = 1;

   - else the following paths[i] [j] should be 0;

# Notes and Tips

