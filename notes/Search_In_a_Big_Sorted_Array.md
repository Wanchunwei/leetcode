# Algorism 

Binary Search 

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
- [704. Binary Search](https://github.com/Wanchunwei/leetcode/blob/master/notes/Binary_Search.md)
- [278. First Bad Version](https://github.com/Wanchunwei/leetcode/blob/master/notes/First_Bad_Version.md)
