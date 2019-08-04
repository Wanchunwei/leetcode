# Algorithm 

Divide Conquer

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 60.10% of Java online submissions for Binary Tree Preorder Traversal.

Memory Usage: 34.8 MB, less than 99.83% of Java online submissions for Binary Tree Preorder Traversal.

## Time spent:

3 min

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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> results = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        if (root == null) {
            return results;
        }
        
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            results.add(node.val);
            if (node.right != null) {
                stack.push(node.right);
            }
            
            if (node.left != null) {
                stack.push(node.left);
            }
        }
        
        return results;
    }
}
```

# Time complexity

O(n)

# Note and tips

