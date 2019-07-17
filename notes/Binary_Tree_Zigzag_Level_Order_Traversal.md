# Algorithm 

BFS

# Better solution 

Currently Best

## Performans:

Runtime: 1 ms, faster than 87.90% of Java online submissions for Binary Tree Zigzag Level Order Traversal.

Memory Usage: 36.4 MB, less than 99.94% of Java online submissions for Binary Tree Zigzag Level Order Traversal.

## Time spent:

19 min 07 seconds

## Times of Wrong answer:

1 - Bug 1

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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> zigzag = new ArrayList<>();
        if (root == null) {
            return zigzag;
        }
        int level = 0;
        
        Deque<TreeNode> queue = new LinkedList<>();
        queue.offerLast(root);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> results = new ArrayList<>();
            level++;
            
            for (int i = 0; i < size; i++) {
                if (level % 2 == 0) {
                    TreeNode node = queue.pollLast();
                    results.add(node.val);
                    if (node.right != null) {
                        queue.offerFirst(node.right);
                    }
                    
                    if (node.left != null) {
                        queue.offerFirst(node.left);
                    }
                } else {
                    TreeNode node = queue.pollFirst();
                    results.add(node.val);
                    if (node.left != null) {
                        queue.offerLast(node.left);
                    }
                    
                    if (node.right != null) {
                        queue.offerLast(node.right);
                    }
                }
            }
            
            zigzag.add(results);
        }
        
        return zigzag;
    }
}
```
# Time complexity
O(V + E)

# Notes and Tips
1. `OfferLast()` and `PollFirst()` in `Deque` is the same as `offer()` and `poll()` in `Queue`.
