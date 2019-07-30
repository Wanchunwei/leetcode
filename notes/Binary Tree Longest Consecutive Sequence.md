# Algorithm 

Divide Conquer (Bottom Up DFS)

Analysis:

1. To find the max value for longest consecutive sequence in Binary Tree, set a global variable `longest` to store the value (go through each subtree).

2. Define divide conquer rule : For each subtree, calculate the longest consecutive sequence start at current root node. To achieve this, we need to know `the value of longest consecutive sequence` start at `root.left` and `root.right`.

3. Calculate the longest consecutive sequence(LCS) start at current root node : 

   - if `root.left or root.right == null` or `root.val != root.left or root.right - 1  ` then the LCS for that subtree should be 0 

   - Select a longer path between left and right and return the path + 1;

4. Dealing with corner cases : In helper If `root == null`, then return 0; In main function If `root == null`, then return 0

5.  Return `longest`

# Better solution

(Top Down DFS)

```java
private int maxLength = 0;
public int longestConsecutive(TreeNode root) {
    dfs(root, null, 0);
    return maxLength;
}

private void dfs(TreeNode p, TreeNode parent, int length) {
    if (p == null) return;
    length = (parent != null && p.val == parent.val + 1) ? length + 1 : 1;
    maxLength = Math.max(maxLength, length);
    dfs(p.left, p, length);
    dfs(p.right, p, length);
}
```



## Performance:

Runtime: 1 ms, faster than 100.00% of Java online submissions for Binary Tree Longest Consecutive Sequence.

Memory Usage: 40.2 MB, less than 98.67% of Java online submissions for Binary Tree Longest Consecutive Sequence.

## Time spent:

42 min 55 seconds

## Times of Wrong answer:

2 - Bug 1, Bug 2

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
    int longest = 1;
    public int longestConsecutive(TreeNode root) {
        //Bug : Remember to consider the null for root;
        if (root == null) {
            return 0;
        }
        
        helper(root);
        return longest;
    }
    
    private int helper(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        int longestLeft = helper(root.left);
        int longestRight = helper(root.right);
        
        if  ((longestLeft == 0 || root.val != root.left.val - 1) 
             && (longestRight == 0 || root.val != root.right.val - 1)) {
            return 1;
        } 

        if (longestLeft == 0 || root.val != root.left.val - 1) {
            if (longest < longestRight + 1) {
                longest = longestRight + 1;
            }
            return longestRight + 1;
        }
        
        if (longestRight == 0 || root.val != root.right.val - 1) {
            //Notation : can replace with longest = longest < longestLeft + 1 ? longestLeft + 1 : longest;
            if (longest < longestLeft + 1) {
                longest = longestLeft + 1;
            }
            return longestLeft + 1;
        }
        
        
        if (longest < Math.max(longestLeft + 1, longestRight + 1)) {
            longest = Math.max(longestLeft + 1, longestRight + 1);
        }
        
        return Math.max(longestLeft + 1, longestRight + 1);  
    }
}
```

# Time complexity

O(n)

# Note and tips

1. Replace simple if condition with condition ? true : false