# Algorithm

Divide Conquer

The key point of this problem is to understand that **this is still a problem of Divide Conquer on Binary Tree**. 

The tricky part is that a list is given rather than a binary tree. But the way to solve it doesn't change. We just need to do some pre-process that separate the left tree and right tree from the list.  The rest are the same. 

## Performance:

Runtime: 192 ms, faster than 85.67% of Python3 online submissions for Number of Ways to Reorder Array to Get Same BST.

Memory Usage: 19.3 MB, less than 5.39% of Python3 online submissions for Number of Ways to Reorder Array to Get Same BST.

## Time spent:

not done

## Solution

```python
class Solution:
    def numOfWays(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return 0
        
        return (self.helper(nums)-1) % (10**9+7)
    
    def helper(self, nums):
        if len(nums) <= 2:
            return 1
        
        left = [v for v in nums if v < nums[0]]
        right = [v for v in nums if v > nums[0]]
        return math.comb(len(left)+len(right), len(right)) * self.helper(left) * self.helper(right)
```

# Time complexity

# Notes and Tips

1. 选出原list符合条件的数重新构造list: `left = [v for v in nums if v < nums[0]]`
2. 计算C(n, k) : `math.comb(n, k)`

