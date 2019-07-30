# Algorithm 

Divide Conquer

# Better solution

Currently Best

## Performance:

Runtime: 7 ms, faster than 22.83% of Java online submissions for Lowest Common Ancestor of a Binary Tree.

Memory Usage: 34.5 MB, less than 11.73% of Java online submissions for Lowest Common Ancestor of a Binary Tree.

## Time spent:

21 min 01 seconds

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
    public class Results {
        TreeNode node;
        boolean p;
        boolean q;
        Results(TreeNode node, boolean x, boolean y) {
            this.node = node;
            p = x;
            q = y;
        }    
        Results() {}
    }
    
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        Results results = helper(root, p, q);
        return results.node;
        
    }
    
    private Results helper(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return new Results(null, false, false);
        }
        
        Results left = helper(root.left, p, q);
        Results right = helper(root.right, p, q);

        if (left.p && left.q) {
            return left;
        }
        
        if (right.p && right.q) {
            return right;
        }
        //Bug 1 : Remember to consider root itself
        if ((left.p || right.p || root.val == p.val) 
            && (left.q || right.q || root.val == q.val)) {
            return new Results(root, true, true);
        }
        
        if (left.p || right.p || root.val == p.val) {
            return new Results(root, true, false);
        }
        
        if (left.q || right.q || root.val == q.val) {
            return new Results(root, false, true);
        }
        
        return new Results(root, false, false);
    }
}
```

# Time complexity

O(n)

# Note and tips

1. Remember to consider **root** itself when process divide conquer.