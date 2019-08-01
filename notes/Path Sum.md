# Algorithm 

Divide conquer

# Better solution

Currently Best

## Performance:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Path Sum.

Memory Usage: 37.9 MB, less than 90.96% of Java online submissions for Path Sum.

## Time spent:

2 min 25 seconds

## Times of Wrong answer:

None

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
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        
        if (root.val == sum && root.left == null && root.right == null) {
            return true;
        }
        
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
}
```

# Time complexity

O(n)

# Note and tips

