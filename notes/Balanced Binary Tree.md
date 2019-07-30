# Algorithm 

Divide Conquer

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 94.34% of Java online submissions for Balanced Binary Tree.

Memory Usage: 38.7 MB, less than 85.57% of Java online submissions for Balanced Binary Tree.

## Time spent:

12 min 03 seconds

## Times of Wrong answer:

1 - Bug 1

# Solution 

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public class Results {
        boolean isBalanced;
        int depth;
        Results(Boolean is, int d) {
            isBalanced = is;
            depth = d;
        }
        Results() {};
    }
    
    public boolean isBalanced(TreeNode root) {
        return helper(root).isBalanced;
    }
    
    private Results helper(TreeNode root) {
        if (root == null) {
            return new Results(true, 0);
        }
        
        Results left = helper(root.left);
        Results right = helper(root.right);
        Results rootResults = new Results();
        if (Math.abs(left.depth - right.depth) <= 1 && left.isBalanced && right.isBalanced) {
            rootResults.isBalanced = true;
        } else {
            rootResults.isBalanced = false;
        }
        
        rootResults.depth = Math.max(left.depth, right.depth) + 1;
        return rootResults;
            
    }
}
```

# Time complexity

O(n)

# Note and tips

1. `Math.abs()` for int , double, long and float 