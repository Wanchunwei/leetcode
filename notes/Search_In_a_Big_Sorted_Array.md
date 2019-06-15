# Algorism 

Binary Search 
Analysis: 
1. Find the start position s 0, end posotion using multiplication.
2. The given array can be divided into two parts `Larger than target` and `Smaller than target`. 
3. The value can split the given array is `target`.
4. Choose "the relationship of target and nums[mid]" as condition.

# Better solution 

Currently Best

# Solution 

## Performans:

Runtime: 2 ms, faster than 100.00% of Java online submissions for Search in a Sorted Array of Unknown Size.

Memory Usage: 39.3 MB, less than 100.00% of Java online submissions for Search in a Sorted Array of Unknown Size.

## Time spent: 

Not done 


```java
class Solution {
    public int search(ArrayReader reader, int target) {
        int pos = 1;
        while (reader.get(pos - 1) < target) {
            pos = pos * 2;
        }
        
        int start = 0, end = pos;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (target == reader.get(mid)) {
                end = mid;
            } else if (target < reader.get(mid)) {
                end = mid;      //Attention
            } else {
                start = mid;
            }
        }
        
        if (reader.get(start) == target) {
            return start;
        }
        
        if (reader.get(end) == target) {
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
- [33 Search in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_in_Rotated_Sorted_Array.md)
- [153 Find Minimum in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Find_Minimum_in_Rotated_Sorted_Array.md)
- [704. Binary Search](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Search.md)
- [278. First Bad Version](https://github.com/Wanchunwei/leetcode/blob/master/notes/First_Bad_Version.md)
