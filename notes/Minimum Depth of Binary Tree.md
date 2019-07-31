# Algorithm 

Divide Conquer

# Better solution

Currently Best

## Performance:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Minimum Depth of Binary Tree.

Memory Usage: 39.1 MB, less than 98.48% of Java online submissions for Minimum Depth of Binary Tree.

## Time spent:

8 min 22 seconds

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
    public int minDepth(TreeNode root) {
        int min = helper(root);
        if(min == Integer.MAX_VALUE) {
            return 0;
        }
        
        return min;
    }
    
    private int helper(TreeNode root) {
        //int max = Integer.MAX_VALUE;
        if (root == null) {
            return Integer.MAX_VALUE;
        }
        
        if (root.left == null && root.right == null) {
            return 1;
        }
        
        return Math.min(helper(root.left), helper(root.right)) + 1;
    }
}8
```

# Time complexity

O(n)

# Note and tips

1. Carefully when encountering leaf node, which stand for  `root.left == null && root.right == null`

