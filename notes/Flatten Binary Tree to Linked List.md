# Algorithm 

Divide conquer

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 50.72% of Java online submissions for Flatten Binary Tree to Linked List.

Memory Usage: 38.2 MB, less than 52.18% of Java online submissions for Flatten Binary Tree to Linked List.

## Time spent:

22 min 35 seconds

## Times of Wrong answer:

none

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
    
    public void flatten(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        helper(queue, root);

        if (!queue.isEmpty()) {
            TreeNode current = queue.poll();
            while(!queue.isEmpty()) {
                TreeNode node = queue.poll();
                current.left = null;
                current.right = node;
                current = node;
            } 
        }
        
                  
    }
    
    private void helper(Queue<TreeNode> queue, TreeNode root) {
        if (root != null) {
            queue.offer(root);
            if (root.left != null) {
                helper(queue, root.left);
            }
        
            if (root.right != null) {
                helper(queue, root.right);
            }  
        }
    }
}
```

# Time complexity

O(n)

# Note and tips