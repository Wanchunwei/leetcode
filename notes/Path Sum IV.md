# Algorithm 

Divide conquer

# Better solution

Currently Best

Simpler and clearer solution:

```java
class Solution {
    int sum = 0;
    Map<Integer, Integer> tree = new HashMap<>();
    
    public int pathSum(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        
        for (int num : nums) {
            int key = num / 10;
            int value = num % 10;
            tree.put(key, value);
        }
        
        traverse(nums[0] / 10, 0);
        
        return sum;
    }
    
    private void traverse(int root, int preSum) {
        int level = root / 10;
        int pos = root % 10;
        int left = (level + 1) * 10 + pos * 2 - 1;
        int right = (level + 1) * 10 + pos * 2;
        
        int curSum = preSum + tree.get(root);
        
        if (!tree.containsKey(left) && !tree.containsKey(right)) {
            sum += curSum;
            return;
        }
        
        if (tree.containsKey(left)) traverse(left, curSum);
        if (tree.containsKey(right)) traverse(right, curSum);
    }
}
```



## Performance:

Runtime: 1 ms, faster than 96.63% of Java online submissions for Path Sum IV.

Memory Usage: 34.5 MB, less than 100.00% of Java online submissions for Path Sum IV.

## Time spent:

1 hour 10 min

## Times of Wrong answer:

None

# Solution 

```java
class TreeNode {
      public int val;
      public TreeNode left, right;
      public TreeNode(int val) {
          this.val = val;
          this.left = this.right = null;
      }
   }
    
class Result {
    public int sum;
    public int numOfPath;
    public Result() {}
    public Result(int sum, int numOfPath) {
        this.sum = sum;
        this.numOfPath = numOfPath;
    }
}

class Solution {
    public int pathSum(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        TreeNode root = new TreeNode(nums[0] % 10);
        int a = nums[0] / 100;
        int b = (nums[0] / 10) % 10;
        constructTree(nums, root, a, b);
        return helper(root).sum;
    }
    
    private void constructTree(int[] nums, TreeNode root, int level, int position) {
        
        root.left = find(level + 1, position*2 -1, nums);
        root.right = find(level + 1, position*2, nums);
        
        if (root.left != null) {
            constructTree(nums, root.left, level + 1, position*2 - 1);
        }

        if (root.right != null) {
            constructTree(nums, root.right, level + 1, position*2);
        }
    }
    
    private TreeNode find(int level, int position, int[] nums) {
        int element = level*100 + position*10;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] >= element && nums[i] <= element + 9) {
                return new TreeNode(nums[i] % 10);
            }
        }
        return null;
    }
    
    private Result helper(TreeNode root) {
        if (root == null) {
            return new Result(0, 0);
        }
        
        if (root.left == null && root.right == null) {
            return new Result(root.val, 1);
        } 
        
        Result left = helper(root.left);
        Result right = helper(root.right);
        
        return new Result(left.sum + right.sum + (left.numOfPath + right.numOfPath)*root.val, 
                          left.numOfPath + right.numOfPath);
    }
}
```

# Time complexity

O(n)

# Note and tips

1. Remember template method  that construct a tree from an array like [113, 215, 221] ---- `constructTree()`.

2. Initiate class without `public` ---   class Result { ... }

   