# Algorithm

DFS

# Better solution

Currently Best

## Performance:

Runtime: 2 ms, faster than 51.99% of Java online submissions for Surrounded Regions.

Memory Usage: 40.8 MB, less than 85.71% of Java online submissions for Surrounded Regions.

## Time spent:

19 min 40 seconds

## Times of Wrong answer:

1 -Bug 1

## Solution

```java
class Solution {
    public void solve(char[][] board) {
        if (board != null) {
            for (int i = 0; i < board.length; i++) {
                for (int j = 0; j < board[0].length; j++) {
                    if (board[i][j] == 'O' && 
                        (i == 0 || i == board.length - 1 || 
                         j == 0 || j == board[0].length - 1)) {
                        dfs(board, i, j);
                    }
                }
            }
            
            for (int i = 0; i < board.length; i++) {
                for (int j = 0; j < board[0].length; j++) {
                    if (board[i][j] == 'O') {
                        board[i][j] = 'X';
                    }
                    
                    if (board[i][j] == '#') {
                        board[i][j] = 'O';
                    }
                }
            }
        }
    }
    
    private void dfs(char[][] board, int i, int j) {
        //Bug 1 : Notice that the condition should be board[i][j] != 'O' not board[i][j] == 'X'
        if (i < 0 || i > board.length - 1 || j < 0 || j > board[0].length - 1 ||
            board[i][j] != 'O' ) {
            return;
        }
        
        board[i][j] = '#';
        dfs(board, i - 1, j);
        dfs(board, i + 1, j);
        dfs(board, i, j - 1);
        dfs(board, i, j + 1);

    }
}
```

# Time complexity

O(n)

# Notes and Tips

1. Notice that the condition whether do DFS should be `board[i][j] != 'O'` not `board[i][j] == 'X'`