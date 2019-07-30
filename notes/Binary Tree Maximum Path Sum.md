# Algorithm 

Divide Conquer

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 99.96% of Java online submissions for Binary Tree Maximum Path Sum.

Memory Usage: 40.7 MB, less than 93.52% of Java online submissions for Binary Tree Maximum Path Sum.

## Time spent:

21 min 20 seconds

## Times of Wrong answer:

4

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
    int max = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        helper(root);
        return max;
    }
    
    private int helper(TreeNode root) {
        int maxPathSum = Integer.MIN_VALUE;
        if (root == null) {
            return 0;
        }
        
        int leftMaxSum = helper(root.left);
        int rightMaxSum = helper(root.right);
        
        //Bus 1 : There are four cases in this step : 1. no left 2. no right 3. no left, no right 4. with left and right
        maxPathSum = Math.max(Math.max(leftMaxSum + rightMaxSum + root.val, root.val),                                 Math.max(rightMaxSum + root.val, leftMaxSum + root.val));
        
        max = max < maxPathSum ? maxPathSum : max;
        
        //Bug 2 : Because the end node can be any node, so we must compare Math.max(leftMaxSum, rightMaxSum) + root.val and root.val, otherswise if we return Math.max(leftMaxSum, rightMaxSum) + root.val directly, the end point must be a leaf.
        return Math.max(Math.max(leftMaxSum, rightMaxSum) + root.val, root.val);
    }
}
```

# Time complexity

O(n)

# Note and tips

1. When encountering problems that `the end node can be any nodes`, then we must remember that whether we can only return root without left and right (Or only with left or right if `start nodes can be any nodes`)

   