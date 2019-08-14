# Algorithm

BFS



Analysis:

This is a typical `Search` problem, either by using `DFS` or `BFS`. Search rules:

1. If click on a mine ('`M`'), mark it as '`X`', stop further search.
2. If click on an empty cell ('`E`'), depends on how many surrounding mine:
    2.1 Has surrounding mine(s), mark it with number of surrounding mine(s), stop further search.
    2.2 No surrounding mine, mark it as '`B`', continue search its `8` neighbors.

# Better solution

DFS : 

Runtime: 1 ms, faster than 88.27% of Java online submissions for Minesweeper.

Memory Usage: 41.6 MB, less than 56.25% of Java online submissions for Minesweeper.

```java
public class Solution {
    public char[][] updateBoard(char[][] board, int[] click) {
        int m = board.length, n = board[0].length;
        int row = click[0], col = click[1];
        
        if (board[row][col] == 'M') { // Mine
            board[row][col] = 'X';
        }
        else { // Empty
            // Get number of mines first.
            int count = 0;
            for (int i = -1; i < 2; i++) {
                for (int j = -1; j < 2; j++) {
                    if (i == 0 && j == 0) continue;
                    int r = row + i, c = col + j;
                    if (r < 0 || r >= m || c < 0 || c < 0 || c >= n) continue;
                    if (board[r][c] == 'M' || board[r][c] == 'X') count++;
                }
            }
            
            if (count > 0) { // If it is not a 'B', stop further DFS.
                board[row][col] = (char)(count + '0');
            }
            else { // Continue DFS to adjacent cells.
                board[row][col] = 'B';
                for (int i = -1; i < 2; i++) {
                    for (int j = -1; j < 2; j++) {
                        if (i == 0 && j == 0) continue;
                        int r = row + i, c = col + j;
                        if (r < 0 || r >= m || c < 0 || c < 0 || c >= n) continue;
                        if (board[r][c] == 'E') updateBoard(board, new int[] {r, c});
                    }
                }
            }
        }
        
        return board;
    }
}
```

## Performance:

Runtime: 4 ms, faster than 10.25% of Java online submissions for Minesweeper.

Memory Usage: 44.2 MB, less than 43.75% of Java online submissions for Minesweeper.

## Time spent:

48 min 57 seconds 

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    public char[][] updateBoard(char[][] board, int[] click) {
        if (board[click[0]][click[1]] == 'M') {
            board[click[0]][click[1]] = 'X';
            return board;
        }
        
        
        int[] directionX = {-1, 0, 1, 1, -1, 1, 0, -1};
        int[] directionY = {1, 1, 1, 0, 0, -1, -1, -1};
        boolean[][] visit = new boolean[board.length][board[0].length];
        Deque<int[]> queue = new LinkedList<>();
        queue.offer(click);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            //Notation : Remember to add for loop here, because once we add all 8  nodes in queue, we should go through all of them next round.
            for (int j = 0; j < size; j++) {
                int[] cur = queue.poll();
                visit[cur[0]][cur[1]] = true;
                int count = 0, validNode = 0;
                for (int i = 0; i < 8; i++) {
                    int y = cur[0] + directionY[i];
                    int x = cur[1] + directionX[i];
                    if (y < 0 || y >= board.length || x < 0 || x >= board[0].length ||
                        visit[y][x]) {
                        continue;
                    }
                    if (board[y][x] == 'M') {
                        count++;
                    }
                    int[] coor = {y, x};
                    queue.offerFirst(coor); 
                    validNode++;
                }
            
                if (count == 0) {
                    board[cur[0]][cur[1]] = 'B';
                } else {
                    board[cur[0]][cur[1]] = (char)(48 + count);
                    for (int i = 0; i < validNode; i++) {
                        queue.pollFirst();
                    }
                }
            }
            
        }
        return board;
    }
    
}
```

# Time complexity

O(n)

# Notes and Tips

1. Remember to add for loop here, because once we add all 8  nodes in queue, we should go through all of them next round.