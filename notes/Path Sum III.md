# Algorithm 

Divide conquer

Analysis:

1. Set `num` as a global variable to store path sum.
2. Define Divide Conquer rule : 
   - For each node, find the paths that start at that node -- `helper2()`.
   - To find the paths ---  `helper()`
3. Dealing with corner cases : if `root == null` return 0, if `root.val == sum`, then return `1 + helper(root.left, 0) + helper(root.right, 0)`

# Better solution

Currently Best

## Performance:

Runtime: 11 ms, faster than 47.34% of Java online submissions for Path Sum III.

Memory Usage: 40.4 MB, less than 70.37% of Java online submissions for Path Sum III.

## Time spent:

Not Done

## Times of Wrong answer:

2

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
    int num = 0;
    public int pathSum(TreeNode root, int sum) {
        helper2(root, sum);
        return num;
    }
    
    private int helper2(TreeNode root, int sum) {
        if (root == null) {
            return 0;
        }
        
        int paths = helper(root, sum);
        num = num + paths;
        
        int left = helper2(root.left, sum);
        int right = helper2(root.right, sum);
        
        return left + right + paths;
    }
    
    private int helper(TreeNode root, int sum) {
        int count = 0;
        if (root == null) {
            return 0;
        }
        
        if (sum == root.val) {
            return 1 + helper(root.left, 0) + helper(root.right, 0);
        }
        
        
        int left = helper(root.left, sum - root.val);
        int right = helper(root.right, sum - root.val);
        
        return left + right;
    }
}
```

# Time complexity

O(n)

# Note and tips

1. Analysis 