# Algorism 

Binary Search 

# Better solution 

Currently Best

# Solution 

## Performans:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Binary Search.

Memory Usage: 38.8 MB, less than 99.08% of Java online submissions for Binary Search.

## Time spent: 

6 min 52 seconds

## Times of debugging:

3

## Times of Wrong answer:

0

```java
class Solution {
    public int search(int[] nums, int target) {
        if(nums == null || nums.length == 0) {// 1. Think less error: if(target == null || nums == null || nums.length == 0)
            return -1; //2. Type error: return -1'
        }
        
        /*
         Coding Style Notation: 
         1. int mid, int start = 0, end = nums.length - 1; //write in one line
        */
        int mid, start = 0;//3. Forget to initiate variable: int start = 0;
        int end = nums.length - 1;
        
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (target == nums[mid]) {
                end = mid;
            } else if (target < nums[mid]) {
                end = mid;
            } else {
                start = mid;
            }
        }
        
        if (target == nums[start]) {
            return start;
        }
        
        if (target == nums[end]) {
            return end;
        }
        
        return -1;
    }
}
```
# Time complexity
O(logn)

# Notes and Tips
1. `start + 1 < end`, in case of endless loop;

2. `start + (end - start) / 2`, in case of integer overflow

3. `A[mid] ==, <, >`, don't merge = and <, show thinking process

4. `A[start] A[end] ? target`


# Relavent Question
- [33 Search in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_in_Rotated_Sorted_Array.md)
- [153 Find Minimum in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Find_Minimum_in_Rotated_Sorted_Array.md)
- [702. Search in a big sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_In_a_Big_Sorted_Array.md)
- [278. First Bad Version](https://github.com/Wanchunwei/leetcode/blob/master/notes/First_Bad_Version.md)