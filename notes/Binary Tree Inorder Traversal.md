# Algorithm 

Divide Conquer

Analysis:

1. Go to the left bottom of current tree and push the node.
2. pop current node and got to `node.right `
3. Repeat the process until `stack.isEmpty() or node == null`

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 56.29% of Java online submissions for Binary Tree Inorder Traversal.

Memory Usage: 35 MB, less than 100.00% of Java online submissions for Binary Tree Inorder Traversal.

## Time spent:

8 min

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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> results = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        if (root == null) {
            return results;
        }
        
        TreeNode node = root; 
        while (!stack.isEmpty() || node != null) {
            while (node != null) {
                stack.push(node);
                node = node.left;
            }
            
            node = stack.pop();
            results.add(node.val);
            node = node.right;
        }
        
        return results;
    }
}
```

# Time complexity

O(n)

# Note and tips

