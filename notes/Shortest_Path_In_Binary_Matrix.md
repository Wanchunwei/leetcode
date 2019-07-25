# Algorithm

BFS

# Better solution 

BFS(with 2D array instead of set<Pair<>>)

Runtime: **21 ms**

Memory Usage: **52.5 MB**

```java
class Solution {
    private int dir[][] = new int[][]{{0,1},{0,-1},{1,0},{-1,0},
                                      {1,-1},{-1,1},{-1,-1},{1,1}};

    public int shortestPathBinaryMatrix(int[][] grid) {

        int m = grid.length;
        int n = grid[0].length;

        if(grid[0][0]==1 || grid[m-1][n-1]==1) {
            return -1;
        }

        boolean[][] visited = new boolean[m][n];
        visited[0][0] = true;
        Queue<int[]> queue = new LinkedList<>();
        queue.add(new int[]{0,0});

        int ans=0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for(int i=0;i<size;i++) {
                int[] pop = queue.remove();
                if(pop[0]==m-1 && pop[1]==n-1) {
                    return ans+1;
                }
                for (int k=0;k<8;k++) {
                    int nextX = dir[k][0]+pop[0];
                    int nextY = dir[k][1]+pop[1];

                    if(nextX>=0 && nextX<m && nextY>=0 && nextY<n 
                       && !visited[nextX][nextY] && grid[nextX][nextY]==0) {
                        queue.add(new int[]{nextX,nextY});
                        visited[nextX][nextY]=true;
                    }

                }
            }
            ans++;
        }

        return -1;
    }
}
```



## Performance:

Runtime: **198 ms**

Memory Usage: **53.8 MB**

## Time spent:

22 min 28 seconds

## Times of Wrong answer:

0

## Solution

```java
import javafx.util.Pair;

class Solution {
    public int shortestPathBinaryMatrix(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0 || 
            grid[0][0] == 1 || grid[grid.length - 1][grid.length - 1] == 1) {
            return -1;
        }
        
        int n = grid.length, steps = 1;
        int[] directionX = {-1, 0, 1, -1, 1, -1, 0, 1};
        int[] directionY = {-1, -1, -1, 0, 0, 1, 1, 1};
        
        Queue<Pair<Integer, Integer>> queue = new LinkedList<>();
        Set<Pair<Integer, Integer>> set = new HashSet<>();
        
        queue.offer(new Pair(0, 0));
        set.add(new Pair(0, 0));
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                Pair<Integer, Integer> node = queue.poll();
                for (int j = 0; j < 8; j++) {
                    Pair<Integer, Integer> next = 
                        new Pair(node.getKey() + directionX[j],                                                  node.getValue() + directionY[j]);
                    if (next.getKey() == n - 1 && next.getValue() == n - 1) {
                        return steps + 1;
                    }
                        
                    if (next.getKey() >= 0 && next.getKey() < n && 
                        next.getValue() >= 0 && next.getValue() < n &&                                   !set.contains(next) &&
                        grid[next.getKey()][next.getValue()] != 1) {
                        queue.offer(next);
                        set.add(next);
                    }
                }
            }
            steps++;
        }
        
        return -1;
    }
}
```

# Time complexity

O(MN)

# Notes and Tips

1. `Pair<>` and `Set<>`is more time consuming  than `array[]`of length 2. Hence using `array[][]` is much more efficient than `Set<Pair<>>` when dealing with 2D Matrix

   

   