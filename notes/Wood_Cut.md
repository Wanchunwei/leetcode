# Algorithm 

Binary Search

Analysis: Binary search for answer

# Better solution 

Currently Best

## Performance:

Total runtime: 463ms

## Time spent:

10  min 16 seconds

## Times of Wrong answer:

None

## Solution

```java
public class Solution {
    /**
     * @param L: Given n pieces of wood with length L[i]
     * @param k: An integer
     * @return: The maximum length of the small pieces
     */
    public int woodCut(int[] L, int k) {
        // write your code here
        if (L.length == 0 || L == null) {
            return 0;
        }
        
        int start = 1, end = 0;
        for (int i = 0; i < L.length; i++) {
            if (L[i] > end) {
                end = L[i];
            } 
        }
        
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (canGet(mid, L, k)) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (canGet(end, L, k)) {
            return end;
        }
        
        if (canGet(start, L, k)) {
            return start;
        }
        
        return 0;
    }
    
    private boolean canGet(int length, int[] L, int k) {
        for (int i = 0; i < L.length; i++) {
            k -= L[i] / length;
        }
        
        if (k <= 0) {
            return true;
        }
        
        return false;
    }
}
```

# Time complexity

O(nlog(Len))

# Notes and Tips

