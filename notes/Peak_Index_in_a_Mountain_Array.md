# Algorism 

Binary Search 

# Better solution 

Currently Best

# Solution 

## Performans:

Runtime: 10 ms, faster than 99.71% of Java online submissions for First Bad Version.

Memory Usage: 33.2 MB, less than 100.00% of Java online submissions for First Bad Version.

## Time spent: 

6 min 46 seconds

# Times of wrong answer:

None

```java
class Solution {
    public int peakIndexInMountainArray(int[] A) {
        if (A == null ||  A.length == 0) {
            return -1;
        }
        
        int start = 0, end = A.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (A[mid] > A[mid - 1] && A[mid] < A[mid + 1]) {
                start = mid;
            } else if (A[mid] < A[mid - 1] && A[mid] > A[mid + 1]) {
                end = mid;
            } else {
                return mid;
            }
        }
        
        if (A[start] > A[start - 1] && A[start] > A[start + 1]) {
            return start;
        }
        
        return end;
     }
}
```

# Time complexity
O(logn)

# Notes and Tips

# Relavent Question
- [33 Search in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_in_Rotated_Sorted_Array.md)
- [153 Find Minimum in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Find_Minimum_in_Rotated_Sorted_Array.md)
- [702. Search in a big sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_In_a_Big_Sorted_Array.md)
- [704. Binary Search](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Search.md)

