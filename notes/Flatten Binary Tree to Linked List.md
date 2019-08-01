# Algorithm 

BFS

# Better solution

Divide conquer (Just remember as a template)

```java
public class Codec {
    public String serialize(TreeNode root) {
        if (root == null) return "#";
        return root.val + "," + serialize(root.left) + "," + serialize(root.right);
    }

    public TreeNode deserialize(String data) {
        Queue<String> queue = new LinkedList<>(Arrays.asList(data.split(",")));
        return helper(queue);
    }
    
    private TreeNode helper(Queue<String> queue) {
        String s = queue.poll();
        if (s.equals("#")) return null;
        TreeNode root = new TreeNode(Integer.valueOf(s));
        root.left = helper(queue);
        root.right = helper(queue);
        return root;
    }
}
```



## Performance:

Total runtime 1849 ms

Your submission beats 9.80% Submissions!

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