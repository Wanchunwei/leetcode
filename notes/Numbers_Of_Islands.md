# Algorithm 

BFS

Analysis:
1. Traverse all grids in the given matrix.
2. For each grid, find the island includes it and cover all grids in the island with '0' `findIslands()` (BFS)
3. Count ++ 

# Better solution 

Rcursion(DFS)

```java
public class Solution {

private int n;
private int m;

public int numIslands(char[][] grid) {
    int count = 0;
    n = grid.length;
    if (n == 0) return 0;
    m = grid[0].length;
    for (int i = 0; i < n; i++){
        for (int j = 0; j < m; j++)
            if (grid[i][j] == '1') {
                DFSMarking(grid, i, j);
                ++count;
            }
    }    
    return count;
}

private void DFSMarking(char[][] grid, int i, int j) {
    if (i < 0 || j < 0 || i >= n || j >= m || grid[i][j] != '1') return;
    grid[i][j] = '0';
    DFSMarking(grid, i + 1, j);
    DFSMarking(grid, i - 1, j);
    DFSMarking(grid, i, j + 1);
    DFSMarking(grid, i, j - 1);
}
```

other solution: (Union find)

## Performans:

Runtime: 4 ms, faster than 21.07% of Java online submissions for Number of Islands.

Memory Usage: 41.2 MB, less than 60.17% of Java online submissions for Number of Islands.

## Time spent:

40 min 46 seconds

## Times of Wrong answer:

2 - Bug 1, Bug 2

## Solution
```java
class Solution {
    public int numIslands(char[][] grid) {
        int numsOfIslands = 0;
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '0') {
                    continue;
                } else {
                    //Tip 1: Use two direction array to simplify code. 
                    int[] directionX = {0, 1, -1, 0};
                    int[] directionY = {1, 0, 0, -1};
                    //Bug 1: Before coding, think about what should be push in queue. In matrix problwm, we should push the coordination of grids into queue. 
                    Queue<int[]> queue = new LinkedList<>();
                    int[] coord = {i, j};
                    queue.offer(coord);
                    while (!queue.isEmpty()) {
                        int[] co = queue.poll();
                        for (int p = 0; p < 4; p++) {
                            int r = co[0] + directionX[p];
                            int c = co[1] + directionY[p];
                    
                            //Bugs 2: Remember to deal with oversteping the boundary.  
                            if ((r < 0 || r >= grid.length) || 
                                (c < 0 || c >=grid[0].length)) {
                                continue;
                            }
                    
                            if (grid[r][c] == '1') {
                                int[] newCoord = {r, c};
                                queue.offer(newCoord);
                                grid[r][c] = '0';
                            }
                        }
                    }
                    numsOfIslands++;
                }
            }
        }
        
        return numsOfIslands;
    }
}
```
# Time complexity
O(mn)

# Notes and Tips
1. Use two direction array to simplify code. 
```java
int[] directionX = {0, 1, -1, 0};
int[] directionY = {1, 0, 0, -1};
```
2. In matrix problwm, we should push the coordination of grids into queue. 
3. Remember to deal with oversteping the boundary in matrix problem. 

# Refactor:
```java
class Solution {
    public int numIslands(char[][] grid) {
        int numsOfIslands = 0;
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (findIslans(grid, i, j)) {
                    numsOfIslands++;
                }
            }
        }
        
        return numsOfIslands;
    }
    
    private boolean findIslans(char[][] grid, int i, int j) {
        if (grid[i][j] == '0') {
            return false;
        } else {
            int[] directionX = {0, 1, -1, 0};
            int[] directionY = {1, 0, 0, -1};
            
            Queue<int[]> queue = new LinkedList<>();
            int[] coord = {i, j};
            queue.offer(coord);
            
            while (!queue.isEmpty()) {
                int[] co = queue.poll();
                for (int p = 0; p < 4; p++) {
                    int r = co[0] + directionX[p];
                    int c = co[1] + directionY[p];
                    
                    if ((r < 0 || r >= grid.length) || 
                        (c < 0 || c >=grid[0].length)) {
                         continue;
                    }
                    
                    if (grid[r][c] == '1') {
                        int[] newCoord = {r, c};
                        queue.offer(newCoord);
                        grid[r][c] = '0';
                    }
                }
            }
            return true;
        }
    }
}
```