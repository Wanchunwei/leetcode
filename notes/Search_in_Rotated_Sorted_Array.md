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

Runtime: 0 ms, faster than 100.00% of Java online submissions for Search in Rotated Sorted Array.

Memory Usage: 35.8 MB, less than 100.00% of Java online submissions for Search in Rotated Sorted Array.

## Time spent: 

18 min 51 seconds

## Times of Wrong answer:

1

```java
class Solution {
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (target > nums[end]) {
                if (nums[mid] < nums[end]) {
                    end = mid;
                } else if (nums[mid] > nums[end] && nums[mid] < target) {
                    start = mid;
                } else {
                    end = mid;
                }
            } else {
                if (nums[mid] > nums[end]) {
                    start = mid;
                } else if (nums[mid] < nums[end] && nums[mid] < target) {
                    start = mid;
                } else {
                    end = mid;
                }
            }
        }
        
        if (nums[start] == target) {
            return start;
        } 
        
        if (nums[end] == target) {
            return end;
        }
        
        return -1;
    }
}
```
# Time complexity
O(logn)

# Notes and Tips


# Relavent Question
- [153 Find Minimum in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Find_Minimum_in_Rotated_Sorted_Array.md)
- [704. Binary Search](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Search.md)
- [702. Search in a big sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_In_a_Big_Sorted_Array.md)
- [278. First Bad Version](https://github.com/Wanchunwei/leetcode/blob/master/notes/First_Bad_Version.md)

