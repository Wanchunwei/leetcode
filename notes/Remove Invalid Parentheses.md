# Algorithm

DFS

Analysis : 

1. Using stack to find the number of Invalid parentheses that  should be removed. 
2. Go through the given string `s`to find all possible removal for each invalid parentheses,.

# Better solution

```java
class Solution {
    public List<String> removeInvalidParentheses(String s) {
        List<String> output = new ArrayList<>();
        removeHelper(s, output, 0, 0, '(', ')');
        return output;
    }

    public void removeHelper(String s, List<String> output, int iStart, int jStart, char openParen, char closedParen) {
        int numOpenParen = 0, numClosedParen = 0;
        for (int i = iStart; i < s.length(); i++) {
            if (s.charAt(i) == openParen) numOpenParen++;
            if (s.charAt(i) == closedParen) numClosedParen++;
            if (numClosedParen > numOpenParen) { // We have an extra closed paren we need to remove
                for (int j = jStart; j <= i; j++) // Try removing one at each position, skipping duplicates
                    if (s.charAt(j) == closedParen && (j == jStart || s.charAt(j - 1) != closedParen))
                    // Recursion: iStart = i since we now have valid # closed parenthesis thru i. jStart = j prevents duplicates
                        removeHelper(s.substring(0, j) + s.substring(j + 1, s.length()), output, i, j, openParen, closedParen);
                return; // Stop here. The recursive calls handle the rest of the string.
            }
        }
        // No invalid closed parenthesis detected. Now check opposite direction, or reverse back to original direction.
        String reversed = new StringBuilder(s).reverse().toString();
        if (openParen == '(')
            removeHelper(reversed, output, 0, 0, ')','(');
        else
            output.add(reversed);
    }
}
```

## Performance:

Runtime: 31 ms, faster than 44.89% of Java online submissions for Remove Invalid Parentheses.

Memory Usage: 41.7 MB, less than 38.04% of Java online submissions for Remove Invalid Parentheses.

## Time spent:

29 min 23 seconds

## Times of Wrong answer:

Bug 1

## Solution

```java
class Solution {
    public List<String> removeInvalidParentheses(String s) {
        List<String> results = new ArrayList<>();
        Stack<Character> stack = new Stack<>();
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) != '(' && s.charAt(i) != ')') {
                continue;
            }
            
            if (!stack.isEmpty() && stack.peek() == '(' && s.charAt(i) == ')') {
                stack.pop();
            } else {
                stack.push(s.charAt(i));
            }
        }
        
        Stack<Character> st = new Stack<>();
        while (!stack.isEmpty()) {
            st.push(stack.pop());
        }
        helper(results, s, st, 0);
        return results;
    }
    
    private void helper(List<String> results, 
                        String s,
                        Stack<Character> stack,
                        int startIndex) {
        if (stack.isEmpty()) {
            if (isValid(s) && !results.contains(s)) {
                results.add(s);
            }
            return;
        }
        
        
        for (int i = startIndex; i < s.length(); i++) {
            char pare = stack.pop();
            if (pare == s.charAt(i)) {
                helper(results, s.substring(0, i) + s.substring(i + 1, s.length()), stack, i );
            }
            stack.push(pare);
        }
    }
    
    //Notation : Must implement  a `isValid` method to check whether current string is valid.
    private boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) != '(' && s.charAt(i) != ')') {
                continue;
            }
            
            if (!stack.isEmpty() && stack.peek() == '(' && s.charAt(i) == ')') {
                stack.pop();
            } else {
                stack.push(s.charAt(i));
            }
        }
        
        return stack.isEmpty();
    }
}
```

# Time complexity

O(n)

# Notes and Tips

1. Must implement  a `isValid` method to check whether current string is valid.