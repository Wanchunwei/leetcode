# Algorithm

Divide Conquer

# Better solution

Simpler and clearer solution: 

```java
public class Solution {
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }
    
    public boolean isValidBST(TreeNode root, long minVal, long maxVal) {
        if (root == null) return true;
        if (root.val >= maxVal || root.val <= minVal) return false;
        return isValidBST(root.left, minVal, root.val) && isValidBST(root.right, root.val, maxVal);
    }
}
```



## Performance:

Runtime: 1 ms, faster than 42.74% of Java online submissions for Validate Binary Search Tree.

Memory Usage: 39.3 MB, less than 80.93% of Java online submissions for Validate Binary Search Tree.

## Time spent:

22 min 

## Times of Wrong answer:

None

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
class Result {
    boolean isBalanced;
    int min;
    int max;
    Result() {}
    Result(boolean isBalanced, int min, int max) {
        this.isBalanced = isBalanced;
        this.min = min;
        this.max = max;
    }
}

class Solution {
    public boolean isValidBST(TreeNode root) {
        return helper(root).isBalanced;
    }
    
    private Result helper(TreeNode root) {
        if (root == null) {
            return new Result(true, Integer.MAX_VALUE, Integer.MIN_VALUE);
        }

        Result left = helper(root.left);
        Result right = helper(root.right);
        Result cur = new Result();
        
        if (left.isBalanced && 
            right.isBalanced && 
            (left.max < root.val || root.left == null) && 
            (root.val < right.min || root.right == null)) {
            cur.isBalanced = true;
            cur.min = Math.min(Math.min(left.min, right.min), root.val);
            cur.max = Math.max(Math.max(left.max, right.max), root.val);
        }
        
        return cur;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

