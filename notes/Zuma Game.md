# Algorithm

DFS



**This problem can not use BFS, because we need to change status of both `board` and `hand` each step (can not do backtracking). BFS can only solve problems that does not need backtracking. **



Key Points  for my solution:

1. If i = 0, then the only choice is to insert character `board.charAt(i)`
2. If i != 0, but `board[i] == board[i - 1]`, then of course we should insert `board[i]`
3. If i != 0 and `board[i] != board[i - 1]`. then we should insert `board[i]` because if we insert `board[i - 1]`, it is the same as insert `board[i - 1]` when i = i - 1.
4. In conclusion, whatever the position we want to insert character, we always insert `board[i]`. 

# Better solution

```java
public class Solution {

int MAXCOUNT = 6;   // the max balls you need will not exceed 6 since "The number of balls in your hand won't exceed 5"

public int findMinStep(String board, String hand) {
    int[] handCount = new int[26];
    for (int i = 0; i < hand.length(); ++i) ++handCount[hand.charAt(i) - 'A'];
    int rs = helper(board + "#", handCount);  // append a "#" to avoid special process while j==board.length, make the code shorter.
    return rs == MAXCOUNT ? -1 : rs;
}
private int helper(String s, int[] h) {
    s = removeConsecutive(s);     
    if (s.equals("#")) return 0;
    int  rs = MAXCOUNT, need = 0;
    for (int i = 0, j = 0 ; j < s.length(); ++j) {
        if (s.charAt(j) == s.charAt(i)) continue;
        need = 3 - (j - i);     //balls need to remove current consecutive balls.
        if (h[s.charAt(i) - 'A'] >= need) {
            h[s.charAt(i) - 'A'] -= need;
            rs = Math.min(rs, need + helper(s.substring(0, i) + s.substring(j), h));
            h[s.charAt(i) - 'A'] += need;
        }
        i = j;
    }
    return rs;
}
//remove consecutive balls longer than 3
private String removeConsecutive(String board) {
    for (int i = 0, j = 0; j < board.length(); ++j) {
        if (board.charAt(j) == board.charAt(i)) continue;
        if (j - i >= 3) return removeConsecutive(board.substring(0, i) + board.substring(j));
        else i = j;
    }
    return board;
}

}
```

## Performance:

Runtime: 58 ms, faster than 6.96% of Java online submissions for Zuma Game.

Memory Usage: 39.7 MB, less than 50.00% of Java online submissions for Zuma Game.

## Time spent:

Not Done

## Times of Wrong answer:

Bug 1

## Solution

```java
class Solution {
    int min = Integer.MIN_VALUE;
    public int findMinStep(String board, String hand) {
        int[] balls = new int[26];
        // Notation 1 : Using hand.charAt(i) - 'A' as index to store character. 
        for (int i = 0; i < hand.length(); i++) {
            balls[hand.charAt(i) - 'A']++;
        }
        
        dfs(board, balls, hand.length());
        if (min == Integer.MIN_VALUE) {
            return -1;
        }
        return hand.length() - min;
    }
    
    private void dfs(String board, int[] balls, int remain) {
        if (board.length() == 0) {
            min = min < remain ? remain : min; 
            return;
        } 
        
        if (remain == 0) {
            return;
        }
        
        for (int i = 0; i < board.length(); i++) {
            if (balls[board.charAt(i) - 'A'] == 0) {
                continue;
            }
            balls[board.charAt(i) - 'A']--;
            String s = board.substring(0, i) + board.charAt(i) + 
                       board.substring(i, board.length());
            s = removeConsecutive(s);
            dfs(s, balls, remain - 1);
            balls[board.charAt(i) - 'A']++;

        }
    }
    
    // Notaion 2 : Remember as a template.
    private String removeConsecutive(String board) {
        for (int i = 0, j = 0; j <= board.length(); ++j) {
            if (j < board.length() && board.charAt(j) == board.charAt(i)) 
                continue;
            if (j - i >= 3) 
                return removeConsecutive(board.substring(0, i) + board.substring(j));
            else i = j;
        }
        return board;
    }
    /*private String refactor(String s) {
        int count = 1;
        int size = s.length();
        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == s.charAt(i - 1)) {
                count++;
            } else {
                if (count >= 3) {
                    s = s.substring(0, i - count) + s.substring(i, s.length());
                    i = i - count;
                    count = 1;
                } else {
                    count = 1;
                } 
            }
            
        }
        
        if (count >= 3) {
            s = s.substring(0, s.length() - count);
        }
        
        if (s.length() == size) {
            return s;
        }
        
        return refactor(s);
    }*/
}
```

# Time complexity

O(n)

# Notes and Tips

1. Using `hand.charAt(i) - 'A'` as index to store character. 

2. Remember the template of remove :

```java
private String removeConsecutive(String board) {
    for (int i = 0, j = 0; j < board.length(); ++j) {
        if (board.charAt(j) == board.charAt(i)) continue;
        if (j - i >= 3) return removeConsecutive(board.substring(0, i) + board.substring(j));
        else i = j;
    }
    return board;
}
```

3. **This problem can not use BFS, because we need to change status of both `board` and `hand` each step (can not do backtracking). BFS can only solve problems that does not need backtracking. **

