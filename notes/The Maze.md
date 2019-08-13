# Algorithm

DFS

Key points : 

1. Define DFS rule ： Find whether exist a path that start from `start[]` to `destination[]` in `Maze[]`
2. Using `visit[]` to store visited points in a path. 

# Better solution

Other Solution : BFS : 

Runtime: **6 ms**

Memory Usage: **46 MB**

```java
class Solution {
    public boolean hasPath(int[][] maze, int[] start, int[] destination) {
        if (maze == null || maze.length == 0 || maze[0].length == 0) {
            return false;
        }
        
        int[] directionX = {0, -1, 0, 1};
        int[] directionY = {1, 0, -1, 0};
        Queue<int[]> queue = new LinkedList<>();
        boolean[][] visit = new boolean[maze.length][maze[0].length];
        queue.offer(start);
        visit[start[0]][start[1]] = true;
        
        while (!queue.isEmpty()) {
            int[] coor = queue.poll();
            for (int i = 0; i < 4; i++) {
                int X = coor[1], Y = coor[0];
                while (X + directionX[i] >= 0 && X + directionX[i] < maze[0].length &&
                       Y + directionY[i]>= 0 && Y + directionY[i] < maze.length && 
                       maze[Y + directionY[i]][X + directionX[i]] != 1) {
                    X = X + directionX[i];
                    Y = Y + directionY[i];
                    
                }
                
    
                if (X == destination[1] && Y == destination[0]) {
                    return true;
                }
                
                                
                int[] newCoor = {Y, X};
                if ((X != coor[1] || Y != coor[0]) && !visit[Y][X]) {
                    queue.offer(newCoor);
                    visit[Y][X] = true;
                    //System.out.println(X + " " + Y);
                }
            }
        }
        
        return false;
    }
}
```

## Performance:

Runtime: 2 ms, faster than 96.41% of Java online submissions for The Maze.

Memory Usage: 46 MB, less than 83.33% of Java online submissions for The Maze.

## Time spent:

27 min 16 seconds 

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    int[] directionX = {0, 1, 0, -1};
    int[] directionY = {1, 0, -1, 0};
    boolean isValid = false;
    public boolean hasPath(int[][] maze, int[] start, int[] destination) {
        boolean[][] visit = new boolean[maze.length][maze[0].length];
        return helper(maze, start, destination,visit);
    }
    
    private boolean helper(int[][] maze, int[] start, int[] destination, boolean[][] visit) {
        if (start[0] == destination[0] && start[1] == destination[1]) {
            return true;
        }
        
        
        visit[start[0]][start[1]] = true;
        for (int i = 0; i < 4; i++) {
            int X = start[1], Y = start[0];
            while (X + directionX[i] >= 0 && X + directionX[i] < maze[0].length &&
                   Y + directionY[i] >= 0 && Y + directionY[i] < maze.length &&
                   maze[Y + directionY[i]][X + directionX[i]] == 0) {
                X = X + directionX[i];
                Y = Y + directionY[i];
            }
            
            if ((X == start[1] && Y == start[0]) || visit[Y][X]) {
                continue;
            }
            

            int[] next = {Y, X};
            if (helper(maze, next, destination, visit)) {
                return true;
            }
            //visit[Y][X] = false;
        }
        
        return false;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

1. Key points