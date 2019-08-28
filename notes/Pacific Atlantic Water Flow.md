# Algorithm

BFS



Analysis :

1. Although this is a problem of collecting a list of nodes, but it is not about printing valid paths but valid nodes, so BFS can solve it.  

# Better Solution

DFS : 

```java
class Result {
    boolean Pacific;
    boolean Atlantic;
    Result() {}
    Result(boolean Pacific, boolean Atlantic) {
        this.Atlantic = Atlantic;
        this.Pacific = Pacific;
    }
}

class Solution {
    int[] directionX = {0, 1, 0, -1};
    int[] directionY = {-1, 0, 1, 0};
    public List<List<Integer>> pacificAtlantic(int[][] matrix) {
        List<List<Integer>> results = new ArrayList<>();
        if (matrix == null || matrix.length == 0) {
            return results;
        }
        boolean[][] visit = new boolean[matrix.length][matrix[0].length];
        boolean[][] valid = new boolean[matrix.length][matrix[0].length];
        valid[0][matrix[0].length - 1] = true;
        valid[matrix.length - 1][0] = true;
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                dfs(matrix, i, j, visit,valid, results);
            }
        }
        
        for (int i = 0; i < valid.length; i++) {
            for (int j = 0; j < valid[0].length; j++) {
                if (valid[i][j]) {
                    List<Integer> position = new ArrayList<>();
                    position.add(i);
                    position.add(j);
                    results.add(position);
                }
            }
        }
        return results;
    }
    
    private Result dfs(int[][] matrix, int i, int j, boolean[][] visit, 
                       boolean[][] valid, List<List<Integer>> results) {
        if ((i == 0 && j == matrix[0].length - 1) ||
            (i == matrix.length - 1 && j == 0) || 
            (j == 0 && j == matrix[0].length - 1) ||
            (i == 0 && i == matrix.length - 1)) {
            valid[i][j] = true;
            return new Result(true, true);
        }
        
        visit[i][j] = true;
        boolean Pacific = false, Atlantic = false;
        //DFS part start
        for (int k = 0; k < 4; k++) {
            int[] neighbour = {i + directionX[k], j + directionY[k]};
            if (neighbour[0] >= 0 && neighbour[0] < matrix.length && 
                neighbour[1] >= 0 && neighbour[1] < matrix[0].length && 
                !visit[neighbour[0]][neighbour[1]] && 
                matrix[neighbour[0]][neighbour[1]] <= matrix[i][j]) {
                if (valid[neighbour[0]][neighbour[1]]) {
                    valid[i][j] = true;
                    visit[i][j] = false;
                    return new Result(true, true);
                }
                Result res = dfs(matrix, neighbour[0], neighbour[1], visit, valid, results);
                Pacific = (Pacific || res.Pacific);
                Atlantic = (Atlantic || res.Atlantic);
            }
        }
        //DFS part end
        visit[i][j] = false;
        
        if (i == 0 || j == 0) {
            if (Atlantic) {
                valid[i][j] = true;
                return new Result(true, true);
            } else {
                return new Result(true, false);
            }
        }
        
        if (i == matrix.length - 1 || j == matrix[0].length - 1) {
            if (Pacific) {
                valid[i][j] = true;
                return new Result(true, true);
            } else {
                return new Result(false, true);
            }
        }
        
        if (Pacific && Atlantic) {
            valid[i][j] = true;
        }
        return new Result(Pacific, Atlantic);
    }
}
```

## Performance:

Runtime: 353 ms, faster than 5.17% of Java online submissions for Pacific Atlantic Water Flow.

Memory Usage: 55.4 MB, less than 7.14% of Java online submissions for Pacific Atlantic Water Flow.

## Time spent:

50 min

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    int[] directionX = {0, 1, 0, -1};
    int[] directionY = {-1, 0, 1, 0};
    public List<List<Integer>> pacificAtlantic(int[][] matrix) {
        List<List<Integer>> results = new ArrayList<>();
        if (matrix == null || matrix.length == 0) {
            return results;
        }
        
        boolean[][] valid = new boolean[matrix.length][matrix[0].length];
        valid[0][matrix[0].length - 1] = true;
        valid[matrix.length - 1][0] = true;
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                //Notation : Remember to maintain a visit array for each node.  
                boolean[][] visit = new boolean[matrix.length][matrix[0].length];
                Queue<int[]> queue = new LinkedList<>();
                int[] coor = {i, j};
                queue.offer(coor);
                visit[i][j] = true;
                
                boolean Pacific = false, Atlantic = false;
                if (i == 0 || j == 0) {
                    Pacific = true;
                }
                
                if (i == matrix.length - 1 || j == matrix[0].length - 1) {
                    Atlantic = true;
                }
                
                while (!queue.isEmpty()) {
                    int[] cur = queue.poll();
                    for (int k = 0; k < 4; k++) {
                        int[] next = {cur[0] + directionX[k], cur[1] + directionY[k]};
                        if (next[0] < 0 || next[0] >= matrix.length ||
                            next[1] < 0 || next[1] >= matrix[0].length || 
                            visit[next[0]][next[1]] || 
                            matrix[next[0]][next[1]] > matrix[cur[0]][cur[1]]) {
                            continue;
                        }
                        
                        if (valid[next[0]][next[1]]) {
                            Pacific = true; 
                            Atlantic = true;
                            break;
                        }
                        
                        if (next[0] == 0 || next[1] == 0) {
                            Pacific = true;
                        }
                        
                        if (next[0] == matrix.length - 1 || next[1] == matrix[0].length - 1) {
                            Atlantic = true;
                        }
                        queue.offer(next);
                        visit[next[0]][next[1]] = true;                        
                    }
                } 
                valid[i][j] = Pacific && Atlantic;
            }
        }
        
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (valid[i][j]) {
                    List<Integer> pos = new ArrayList<>();
                    pos.add(i);
                    pos.add(j);
                    results.add(pos);
                }
            }
        }
        return results;
    } 
}
```

# Time complexity

O((m*n)^2)

# Notes and Tips

1. Although this is a problem of collecting a list of nodes, but it is not about printing valid paths but valid nodes, so BFS can solve it.  