# Algorithm 

Divide Conquer

Analysis:

Three cases to consider :

1. `prev = null` or `prev` is the parent of `current`

   Keep going down, always push left to stack first, otherwise right.

2. `prev` is the left children of `current `

   After add left bottom node, check whether right bottom node exist.

3. `prev == current` or `pev` is the right children of `current` 

   Add left bottom node and right bottom node. 

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 63.25% of Java online submissions for Binary Tree Postorder Traversal.

Memory Usage: 34.9 MB, less than 100.00% of Java online submissions for Binary Tree Postorder Traversal.

## Time spent:

14 min

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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> results = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        if (root == null) {
            return results;
        }
        
        TreeNode current = root;
        TreeNode prev = null;
        
        stack.push(root);
        while (!stack.isEmpty()) {
            current = stack.peek();
            if (prev == null || prev.left == current || prev.right == current) {
                if (current.left != null) {
                    stack.push(current.left);
                } else if (current.right != null){
                    stack.push(current.right);
                }
            } else if (current.left == prev) {
                if (current.right != null) {
                    stack.push(current.right);
                }
            } else {
                results.add(current.val);
                stack.pop();
            }
            prev = current;
        }
        
        return results;
    }
}
```

# Time complexity

O(n)

# Note and tips

