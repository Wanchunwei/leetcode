# Algorithm 

BFS

# Better solution 

Currently Best

## Performance:

Runtime: 287 ms, faster than 5.90% of Java online submissions for Shortest Distance from All Buildings.

Memory Usage: 53.1 MB, less than 7.69% of Java online submissions for Shortest Distance from All Buildings.

## Time spent:

35 min

## Times of Wrong answer:

1 - Bug 1

## Solution

```java
class Solution {
    public int shortestDistance(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return -1;
        }
        
        int[] directionX = {0, 1, 0, -1};
        int[] directionY = {1, 0, -1, 0};
        int min = Integer.MAX_VALUE, numOfHouse = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 1) {
                    numOfHouse++;
                }
            }
        }
        
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 2 || grid[i][j] == 1) {
                    continue;
                }
                
                int distance = 0, numOfhouse = 0, dis = 1;
                int[] coor = {i, j};
                boolean[][] visit = new boolean[grid.length][grid[0].length];
                Queue<int[]> queue = new LinkedList<>();
                queue.offer(coor);
                visit[i][j] = true;
                while (!queue.isEmpty()) {
                    int size = queue.size();
                    for (int q = 0; q < size; q++) {
                        int[] cur = queue.poll();
                        for (int p = 0; p < 4; p++) {
                            int[] neighbour = {cur[0] + directionX[p], cur[1] + directionY[p]};
                            if (neighbour[0] < grid.length && neighbour[0] >= 0 && 
                                neighbour[1] < grid[0].length && neighbour[1] >= 0 && 
                                !visit[neighbour[0]][neighbour[1]]) {
                                if (grid[neighbour[0]][neighbour[1]] == 0) {
                                    queue.offer(neighbour);
                                } else if (grid[neighbour[0]][neighbour[1]] == 1) {
                                    numOfhouse++;
                                    distance = distance + dis;
                                    if (numOfhouse == numOfHouse) {
                                        min = min > distance ? distance : min;
                                    }
                                }
                                //Bug 1 : Remember to change visit to true even if grid[neighbour[0]][neighbour[1]] == 1, otherwise whether we don't know the houses we meet are different
                                visit[neighbour[0]][neighbour[1]] = true;
                            }
                        }
                    }
                    dis++;
                }
            }
        }
        
        if (min == Integer.MAX_VALUE) {
            return -1;
        }
        return min;
    }
}
```

# Time complexity

O((MN)^2)

# Notes and Tips

1. Remember to change visit to true even if `grid[neighbour[0]][neighbour[1]] == 1` ,otherwise whether we don't know the houses we meet are different