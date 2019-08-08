# Algorithm

Inorder traversal (iterative)

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 68.68% of Java online submissions for Kth Smallest Element in a BST.

Memory Usage: 38 MB, less than 97.25% of Java online submissions for Kth Smallest Element in a BST.

## Time spent:

6 min 46 seconds

## Times of Wrong answer:

1 -Bug 1

## Solution

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
    public int kthSmallest(TreeNode root, int k) {
        Stack<TreeNode> stack = new Stack<>();
        TreeNode node = root;
        
        while (!stack.isEmpty() || node != null) {
            while (node != null) {
                stack.push(node);
                node = node.left;
            }
            
            node = stack.pop();
            k--;
            if (k == 0) {
                return node.val;
            }
            // Bug 1 : No condition
            node = node.right;
            
        }
        
        return 0;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

