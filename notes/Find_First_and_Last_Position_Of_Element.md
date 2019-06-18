# Algorism 

Binary Search 

Analysis: Apply binary search twice.

# Better solution 

Currently Best

# Solution 

## Performans: 
Runtime: 0 ms, faster than 100.00% of Java online submissions for Find First and Last Position of Element in Sorted Array.

Memory Usage: 42.9 MB, less than 72.10% of Java online submissions for Find First and Last Position of Element in Sorted Array.

## Time spent: 

12 min 57 seconds

## Times of Wrong answer:

No

## Times of debbug:

4

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] position = {-1, -1}; 
        if (nums == null || nums.length == 0) {
            return position;
        }
        
        int startfirst = 0, endfirst = nums.length - 1;
        while (startfirst + 1 < endfirst) {
            int mid = startfirst + (endfirst - startfirst) / 2;
            if (nums[mid] == target) {
                endfirst = mid;
            } else if (nums[mid] > target) {
                endfirst = mid;
            } else {
                startfirst = mid;
            }
        }
        
        if (nums[startfirst] == target) {
            position[0] = startfirst;
        } else if (nums[endfirst] == target) {
            position[0] = endfirst;
        } else {
            return position;
        }
        
        int startlast = 0, endlast = nums.length - 1;
        while (startlast + 1 < endlast) {
            int mid = startlast + (endlast - startlast) / 2;
            if (nums[mid] == target) {
                startlast = mid;
            } else if (nums[mid] > target) {
                endlast = mid;
            } else {
                startlast = mid;
            }
        }
        
        if (nums[endlast] == target) {
            position[1] = endlast;
        } else if (nums[startlast] == target) {
            position[1] = startlast;
        } else {
            return position;
        }
        
        return position;
        
    }
}
```
# Time complexity
O(logn)

# Notes and Tips
1. 3 initialization method of java array: 

           int[] array = { 1, 2, 3, 4 };

           int[] array1 = new int[] { 1, 2, 3, 4 };

           int[] array = new int[3]; (Can not be used with method 1 and 2)

# Relavent Question
- [153 Find Minimum in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Find_Minimum_in_Rotated_Sorted_Array.md)
- [704. Binary Search](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Search.md)
- [702. Search in a big sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_In_a_Big_Sorted_Array.md)
- [278. First Bad Version](https://github.com/Wanchunwei/leetcode/blob/master/notes/First_Bad_Version.md)
