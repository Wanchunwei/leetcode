# Algorithm 

Divide Conquer (Bottom up DFS)

# Better solution

Currently Best

## Performance:

Total runtime 2570 ms

Your submission beats 70.20% Submissions!

## Time spent:

33 min 38 seconds

## Times of Wrong answer:

3 - Bug 1, Bug 2, Bug 3

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
    /*
     * @param root: the root of binary tree
     * @param target: An integer
     * @return: all valid paths
     */
    public List<List<Integer>> binaryTreePathSum(TreeNode root, int target) {
        // write your code here
        List<List<Integer>> results = helper(root, target);
        return results;
    }
    
    private List<List<Integer>> helper(TreeNode root, int target) {
        //Bug 1 : Remember to initialize at the beginning
        List<List<Integer>> tem = new ArrayList<>();
        //Bug 2 : Done't assume target > 0
        if (root == null) {
            return tem;
        }
        
        //Bug 3 : Carefully look at the defination : A valid path is from root node to any of the leaf nodes. Must adding root.left == null && root.right == null to ensure the endpoint is a leaf node.
        if (root.val == target && root.left == null && root.right == null) {
            List<Integer> re = new ArrayList<>();
            re.add(root.val);
            tem.add(re);
            return tem;
        }
        
        List<List<Integer>> tempLeft = helper(root.left, target - root.val);
        List<List<Integer>> tempRight = helper(root.right, target - root.val);
        
        for (List<Integer> list : tempLeft) {
            List<Integer> temp = new ArrayList<Integer>();
            temp.add(root.val);
            for (Integer node : list) {
                temp.add(node);
            }
            tem.add(temp);
        }
        
        for (List<Integer> list : tempRight) {
            List<Integer> temp = new ArrayList<Integer>();
            temp.add(root.val);
            for (Integer node : list) {
                temp.add(node);
            }
            tem.add(temp);
        }
        
        return tem;
    }
}
```

# Time complexity

O(n)

# Note and tips

1. Carefully look at the defination : A valid path is from root node to any of the leaf nodes. Must adding `root.left == null && root.right == null` to ensure the endpoint is a leaf node.