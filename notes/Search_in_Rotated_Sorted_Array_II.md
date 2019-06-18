# Algorism 

Binary Search 

Analysis: 
1. Find the start position is 0, end position is nums.length - 1.
2. The given array can be divided into two parts, `rotated` and `unrotated`. 
3. The value can split the given array is `nums[]end` and target.
4. Choose "the relationship among nums[end], nums[mid] and target" as condition 

# Better solution 

Currently Best

# Solution 

## Performans:
Runtime: 0 ms, faster than 100.00% of Java online submissions for Search in Rotated Sorted Array II.

Memory Usage: 39.6 MB, less than 39.69% of Java online submissions for Search in Rotated Sorted Array II.

## Time spent: 

40 min

## Times of Wrong answer:

4 

Reason: Didn't find the main difficulty of this problem. I should first discuss whether `nums[mid] == nums[end]`, `nums[mid] == target` and `nums[end] == target`. Then the remaining work is the same as problem version I;

```java
class Solution {
    public boolean search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return false;
        }
        
        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[end] == target || nums[mid] == target) {
                return true;
            } else if (nums[mid] == nums[end]) {
                end--;
            } else if (nums[mid] > target) {
                if (target < nums[end] && nums[end] < nums[mid]) {
                    start = mid;
                } else {
                    end = mid;
                }
            } else {
                if (nums[mid] < nums[end] && nums[end] < target) {
                    end = mid;
                } else {
                    start = mid;
                }
            }
        }
        
        if (nums[start] == target) {
            return true;
        }
        
        if (nums[end] == target) {
            return true;
        }
        
        return false;
    }
}
```
# Time complexity
O(logn)

# Notes and Tips
1. Comparing with previous problem I, the main difficulty of this problem is to figure out whether nums[mid] belongs to rotated part or unrotated part when nums[mid] == nums[end]. One simple solutiion is that just do end-- if nums[mid] == nums[end], until nums[mid] != nums[end].

# Relavent Question
- [153 Find Minimum in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Find_Minimum_in_Rotated_Sorted_Array.md)
- [704. Binary Search](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Search.md)
- [702. Search in a big sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_In_a_Big_Sorted_Array.md)
- [278. First Bad Version](https://github.com/Wanchunwei/leetcode/blob/master/notes/First_Bad_Version.md)
