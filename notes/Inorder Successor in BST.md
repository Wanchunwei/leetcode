# Algorithm 

Divide Conquer

# Better solution

```java
public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
    TreeNode res = null;
    while(root!=null) {
        if(root.val > p.val) {
        	res = root;
        	root = root.left;
        }
        else root = root.right;
    }
    return res;
}
```



## Performance:

Runtime: 5 ms, faster than 5.40% of Java online submissions for Inorder Successor in BST.

Memory Usage: 36.7 MB, less than 5.12% of Java online submissions for Inorder Successor in BST.

## Time spent:

21 min

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
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (root == null || (root.left == null && root.right == null)) {
            return null;
        }
        
        boolean isSuccessor = false;
        Stack<TreeNode> stack = new Stack<>();
        //ArrayList<TreeNode> results = new ArrayList<>();
        TreeNode node = root;
        
        while (!stack.isEmpty() || node != null) {       
            while (node != null) {
                stack.push(node);
                node = node.left;
            }
            
            node = stack.pop();
            if (isSuccessor) {
                return node;
            }
            
            if (node.val == p.val) {
                isSuccessor = true;
            }
            
            //results.add(node);
            node = node.right;
        }

        
        return null;
        
    }
}
```

# Time complexity

O(n)

# Note and tips

