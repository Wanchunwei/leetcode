# Algorithm 

Divide Conquer



Analysis : 

1.  To find the longest consecutive sequence, set a global value `max`

2. Define divide conquer rule: 

   - For each root, find `the longest consecitive path` that go through the root.

   - To achieve it, we must get return value : the `longest down path` that start  from `root.left or root.right`and `longest up path` end at `root.left or root.right`

   - There are 4 case for `root.left and root.right` : 

     `null`,  `val == root.val + 1`, `val == root.val - 1`, `val != root.val + 1 && val != root.val - 1` 

     which matches value :

     `0`, `Left(right) LongestUplength`, `Left(right) LongestDwnLength`, `0`

   - To deal with 4 cases, refer to Notation 1

3. Dealing with corner cases : In helper If `root == null`, then return `Results(0, 0)` 

4. return `max`

# Better solution

Currently Best

Simpler and more clearer solution : 

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
class ResultType {
    public int max_length, max_down, max_up;
    ResultType(int len, int down, int up) {
        max_length = len;
        max_down = down;
        max_up = up;    
    }
}

public class Solution {
    /**
     * @param root the root of binary tree
     * @return the length of the longest consecutive sequence path
     */
    public int longestConsecutive2(TreeNode root) {
        // Write your code here
        return helper(root).max_length;
    }
    
    ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(0, 0, 0);
        }

        ResultType left = helper(root.left);
        ResultType right = helper(root.right);

        int down = 0, up = 0;
        
        //Notation 1 : The way to deal with
        if (root.left != null && root.left.val + 1 == root.val)
            down = Math.max(down, left.max_down + 1);

        if (root.left != null && root.left.val - 1 == root.val)
            up = Math.max(up, left.max_up + 1);

        if (root.right != null && root.right.val + 1 == root.val)
            down = Math.max(down, right.max_down + 1);

        if (root.right != null && root.right.val - 1 == root.val)
            up = Math.max(up, right.max_up + 1);

        int len = down + 1 + up;
        len = Math.max(len, Math.max(left.max_length, right.max_length));

        return new ResultType(len, down, up);
    }
}
```



## Performance:

Runtime: 1 ms, faster than 99.45% of Java online submissions for Binary Tree Longest Consecutive Sequence II.

Memory Usage: 38.6 MB, less than 45.94% of Java online submissions for Binary Tree Longest Consecutive Sequence II.

## Time spent:

Not Done

## Times of Wrong answer:

3 

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
        int TopToDown;
        int DownToTop;
        Results() {}
        Results(int TopToDown, int DownToTop) {
            this.DownToTop = DownToTop;
            this.TopToDown = TopToDown;
        }
    }
    
    int max = 0;
    public int longestConsecutive(TreeNode root) {
        helper(root);
        return max;
    }
    
    private Results helper(TreeNode root) {
        if (root == null) {
            return new Results(0, 0);
        }
        
        Results left = helper(root.left);
        Results right = helper(root.right);
        Results results = new Results();
        
        if (((root.left != null && root.left.val != root.val + 1) || root.left == null)
            && ((root.right != null && root.right.val != root.val + 1) || root.right == null))         {
            results.DownToTop = 1;
        } else if ((root.left != null && root.left.val != root.val + 1) 
                   || root.left == null) {
            results.DownToTop = right.DownToTop + 1;
        } else if ((root.right != null && root.right.val != root.val + 1)
                   || root.right == null){
            results.DownToTop = left.DownToTop + 1;
        } else {
            results.DownToTop = Math.max(left.DownToTop, right.DownToTop) + 1;
        }
        
        if (((root.left != null && root.left.val != root.val - 1) || root.left == null)
            && ((root.right != null && root.right.val != root.val - 1) || root.right == null))         {
            results.TopToDown = 1;
        } else if ((root.left != null && root.left.val != root.val - 1) 
                   || root.left == null) {
            results.TopToDown = right.TopToDown + 1;
        } else if ((root.right != null && root.right.val != root.val - 1) 
                   || root.right == null){
            results.TopToDown = left.TopToDown + 1;
        } else {
            results.TopToDown = Math.max(left.TopToDown, right.TopToDown) + 1;
        }
        
        max = max < results.TopToDown + results.DownToTop - 1 ? 
                            results.TopToDown + results.DownToTop - 1 : max;
        
        return results;
    }
}
```

# Time complexity

O(n)

# Note and tips

1. When dealing with divide and conquer, find all the cases that `root.left` and `root.right` may have and its corresponding value. Then do if else judgment. 

