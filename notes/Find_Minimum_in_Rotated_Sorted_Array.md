# Algorism 

Binary Search 

Analysis: 
1. Find the start position is 0, end position is nums.length - 1.
2. The given array can be divided into two parts, `rotated` and `unrotated`. 
3. The value can split the given array is `nums[end]` and `nums[start]`.
4. Choose "the relationship between `nums[mid]` and `nums[end]`" as condition. Because in the special case that no elements rotated, `nums[start]` won't work.

# Better solution 

Currently Best

# Solution 

## Performans:
Runtime: 0 ms, faster than 100.00% of Java online submissions for Find Minimum in Rotated Sorted Array.

Memory Usage: 38.1 MB, less than 66.22% of Java online submissions for Find Minimum in Rotated Sorted Array.

## Time spent: 

9 min 26 seconds

## Times of Wrong answer:

1. Wrongly return `end` instead of `nums[end]`. Should be clear with return value when reading the question. 


```java
class Solution {
    public int findMin(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int start = 0, end = nums.length - 1;
        if (nums[start] < nums[end]) {
            return nums[start];
        }
        
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] > nums[end]) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (nums[start] < nums[end]) {
            return nums[start];
        }
        
        return nums[end]; 
    }
}
```

# Time complexity
O(logn)

# Notes and Tips


# Relavent Question
- [33 Search in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_in_Rotated_Sorted_Array.md)
- [704. Binary Search](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Search.md)
- [702. Search in a big sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_In_a_Big_Sorted_Array.md)
- [278. First Bad Version](https://github.com/Wanchunwei/leetcode/blob/master/notes/First_Bad_Version.md)

