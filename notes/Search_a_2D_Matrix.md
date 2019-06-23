# Algorism 

Binary Search 

Analysis: 

1. Convert matrix index into array index when applying binary search;

# Better solution 

Currently Best

# Solution 

## Performans:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Search a 2D Matrix.

Memory Usage: 43.3 MB, less than 5.02% of Java online submissions for Search a 2D Matrix.

## Time spent: 

Not Done

Reason: Bug1, Bug2.

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0) {
            return false;
        }
        
        int m = matrix.length, n = matrix[0].length;
        
        if (n == 0) {
            return false;
        }
        
        int startrow = 0, startcol = 0;
        int endrow = m - 1, endcol = n - 1;
        
        //Bug1: Suppose to use condition after converting matrix index into array index,  not (startrow == endrow && startcol + 1 < endcol)
        while (startrow * n + startcol + 1 < endrow * n + endcol) { 
            int mid = (endrow * n + endcol + startrow * n + startcol) / 2;

            //Bug2: No matter whether (mid % n == 0), midcol and midrow shouldn't be changed by condition.  
            int midcol = mid % n, midrow = mid / n;
  
            if (matrix[midrow][midcol] < target) {
                startrow = midrow;
                startcol = midcol;
            } else {
                endrow = midrow;
                endcol = midcol;
            }
        }
        
        if (matrix[startrow][startcol] == target) {
            return true;
        }
         
        if (matrix[endrow][endcol] == target) {
            return true;
        }
        
        return false;
        
    }
}
```
# Time complexity
O(logmn)

# Notes and Tips
Bug1

Bug2

# Relavent Question
- [153 Find Minimum in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Find_Minimum_in_Rotated_Sorted_Array.md)
- [704. Binary Search](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Search.md)
- [702. Search in a big sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_In_a_Big_Sorted_Array.md)
- [278. First Bad Version](https://github.com/Wanchunwei/leetcode/blob/master/notes/First_Bad_Version.md)

