# Algorithm 

Divide Conquer (Bottom up DFS)

# Better solution

Currently Best

## Performance:

Total runtime 352 ms

Your submission beats 35.20% Submissions!

## Time spent:

6 min 40 seconds

## Times of Wrong answer:

None

# Solution 

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param root: the root of the binary tree
     * @return: all root-to-leaf paths
     */
    public List<String> binaryTreePaths(TreeNode root) {
        // write your code here
        List<String> results = helper(root);
        return results;
    }
    
    private List<String> helper(TreeNode root) {
        List<String> results = new ArrayList<>();
        if (root == null) {
            return results;
        }
        
        if (root.left == null && root.right == null) {
            results.add("" + root.val);
        }
        
        List<String> leftResults = helper(root.left);
        List<String> rightResults = helper(root.right);
        
        for (String path : leftResults) {
            results.add("" + root.val + "->" + path);
        }
        
        for (String path : rightResults) {
            results.add("" + root.val + "->" + path);
        }
        
        return results;
    }
}
```

# Time complexity

O(n)

# Note and tips

