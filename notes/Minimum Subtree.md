# Algorithm 

Divide Conquer

# Better solution 

Currently Best

## Performance:


Total runtime 201 ms

Your submission beats 58.60% Submissions!

## Time spent:

7 min 40 seconds

## Times of Wrong answer:

None

# Solution 

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param root: the root of binary tree
     * @return: the root of the minimum subtree
     */
    int min = Integer.MAX_VALUE;
    TreeNode minNode;
    public TreeNode findSubtree(TreeNode root) {
        // write your code here
        minNode = root;
        helper(root);
        return minNode;
    }
    
    private int helper(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int sum =  helper(root.left) + helper(root.right) + root.val;
        if (sum < min) {
            min = sum;
            minNode = root;
        }
        
        return sum;
    }
}
```

# Time complexity

O(n) --- n is the number of all nodes in this tree

# Note and tips

