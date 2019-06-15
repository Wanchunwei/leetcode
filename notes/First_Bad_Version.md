# Algorism 

Binary Search 

# Better solution 

Currently Best

# Solution 

## Performans:

Runtime: 10 ms, faster than 99.71% of Java online submissions for First Bad Version.

Memory Usage: 33.2 MB, less than 100.00% of Java online submissions for First Bad Version.

## Time spent: 

6 min 52 seconds

## Times of debugging:

1

# Times of wrong answer:

3

```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int start = 0, end = n;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            
            if (isBadVersion(mid)) {
                end = mid;
            } else {
                start = mid;
            }
        }
        
        if (isBadVersion(start)) {
            return start;
        }
        
        return end;
        
    }
}
```

# Time complexity
O(logn)

# Notes and Tips
1. 
```java
if (isBadVersion(start)) {
            return start;
        }
        
        return end;
```
Directly return end if don't return start, otherwise there is an error that no return statment.

# Relavent Question
- [33 Search in Rotated Sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_in_Rotated_Sorted_Array)
- [702. Search in a big sorted Array](https://github.com/Wanchunwei/leetcode/blob/master/notes/Search_In_a_Big_Sorted_Array.md)
- [704. Binary Search](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Search.md)
