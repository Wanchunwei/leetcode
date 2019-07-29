# Algorithm 

Divide Conquer

Analysis:

1. To Find the max(min) for some value in Binary Tree, a common way is to  initiate a  global value and calculate `the value`(average value in this problem) for `each subtree`(go through all subtree). 
2. In this question, to calculate the average value for current tree, we need to get the `number of nodes` and the `sum of the tree` from return value of `left subtree` and `right subtree`. So we define a new class `TreeInfo`
3. Dealing with corner cases. if the tree is null, then we should return a `Treeinfo` with sum and nums = 0
4. After go through the tree, `return max` 



# Better solution 

Currently Best

## Performance:

Runtime: 1 ms, faster than 94.33% of Java online submissions for Maximum Average Subtree.

Memory Usage: 36.6 MB, less than 100.00% of Java online submissions for Maximum Average Subtree.

## Time spent:

Not Done

## Times of Wrong answer:

Many (Wrong way)

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
    private double max = (double) Integer.MIN_VALUE;
    public class TreeInfo {
        TreeNode node;
        double sum;
        double nums;
        TreeInfo(TreeNode x) {
            node = x;
        }
    }
    
    public double maximumAverageSubtree(TreeNode root) {
        helper(root);
        return max;
    }
    
    private TreeInfo helper(TreeNode root) {
        if (root == null) {
            TreeInfo temp = new TreeInfo(root);
            temp.sum = 0;
            temp.nums = 0;
            return temp;
        }
        
        TreeInfo leftMax = helper(root.left);
        TreeInfo rightMax = helper(root.right);
        TreeInfo tree = new TreeInfo(root);
        
        tree.sum = leftMax.sum + rightMax.sum + root.val;
        tree.nums = leftMax.nums + rightMax.nums + 1;
        double average = tree.sum / tree.nums;
            
        if (max < average) {
            max = average;
        }
        
        return tree;
    }
}
```

# Time complexity

O(n) --- n is the number of all nodes in this tree

# Note and tips

1. `Integer.MIN_VALUE` and `Integer.MAX_VALUE` stand for the min and max value for integer in java
2. When dealing with max(min) value problem with divide conquer, it is a good way to initiate an global value like `max` to store it.