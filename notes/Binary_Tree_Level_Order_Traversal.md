# Algorism 

BFS

# Better solution 

Currently Best

# Solution 

## Performans:

Runtime: 1 ms, faster than 84.11% of Java online submissions for Binary Tree Level Order Traversal.

Memory Usage: 36.1 MB, less than 99.98% of Java online submissions for Binary Tree Level Order Traversal.

## Time spent:

11 min 42 seconds

## Times of Wrong answer

1 - Bug 1

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> results = new ArrayList<>();
        if (root == null) {
            return results;
        }
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            List<Integer> level = new ArrayList<>(); 
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                level.add(node.val);
                if (node.left != null) {
                    queue.offer(node.left);
                }
                
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            
            results.add(level);
        }
        //Bug 1: Remember to return results.
        return results;
    }
}
```
# Time complexity
O(n)

# Notes and Tips
1. `Queue` is an interface, which can be initialized by `LinkedList`;
2. Use `queue.offer()` and `queue.poll()` rather than `queue.add()` and `queue.remove()`;
3. Get size of `Queue` by `queue.size()`;