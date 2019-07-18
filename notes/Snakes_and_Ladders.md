# Algorithm 

BFS

# Better solution 

Currently Best

## Performance:

Runtime: 9 ms, faster than 52.45% of Java online submissions for Snakes and Ladders.

Memory Usage: 37.8 MB, less than 99.80% of Java online submissions for Snakes and Ladders.

## Time spent:

Not Done

## Times of Wrong answer:

Many

## Solution

```java
class Solution {
    public int snakesAndLadders(int[][] board) {
        int n = board.length;
        ArrayList[] nodes = new ArrayList[n*n];
        Queue<Integer> queue = new LinkedList<>();
        //Notation1 : Using Set in case that the graph may contain cycle. 
        Set<Integer> set = new HashSet<>();
        queue.offer(1);
        set.add(1);
        int steps = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                int node = queue.poll();
                for (int j = 1; j <= 6; j++) {
                    if (node + j > n*n) {
                        break;
                    }
                    int[] map = getCoord(node + j, board);
                    if (node + j == n*n || board[map[0]][map[1]] == n*n) {
                        return ++steps;
                    }
                    
                    if (board[map[0]][map[1]] == -1) {
                        if (!set.contains(node + j)) {
                            queue.offer(node + j);
                            set.add(node + j);
                        }
                    } else {
                        if (!set.contains(board[map[0]][map[1]])) {
                            queue.offer(board[map[0]][map[1]]); 
                            set.add(board[map[0]][map[1]]);
                        }
                    }
                }
            }
            steps++;
        }
        
        return -1;
    }
    
    private int[] getCoord(int index, int[][] board) {
        int n = board.length;
        int[] map = new int[2];
        map[0] = n - (index / n) - 1;
        //Notation2 : Notice (index / n) % 2 == 0 and (index % n) == 0 when converting                         coordination.
        if (((index / n) % 2 == 0 && (index % n) != 0) || 
            ((index / n) % 2 == 1 && index % n == 0)) {    
            if ((index % n) == 0) {
                map[0] = n - (index / n);
                map[1] = n - 1;
            } else {
                map[0] = n - (index / n) - 1;
                map[1] = (index % n) - 1;   
            }
        } else {
            if ((index % n) == 0) {
                map[0] = n - (index / n);
                map[1] = 0;
            } else {
                map[0] = n - (index / n) - 1;
                map[1] = n - (index % n);
            }

        }
        return map;
    }
}
```

# Time complexity

O(n^2)

# Notes and Tips

1. Using Set in case that the graph may contain cycle. 
2. Notice (index / n) % 2 == 0 and (index % n) == 0 when converting coordination.