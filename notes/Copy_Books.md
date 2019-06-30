# Algorism 

Binary Search 


Analysis : 
1. Define and find the start point and end point of the problem. 
2. Find the condition that can differentiate our guess point (mid).
3. Carefully think about edge cases.

# Better solution 

Currently Best

# Solution 

## Time spent: 

26 min 55 seconds

# Times of wrong answer:

7


```java
public class Solution {
    /**
     * @param pages: an array of integers
     * @param k: An integer
     * @return: an integer
     */
    public int copyBooks(int[] pages, int k) {
        // write your code here
        if (pages == null || pages.length == 0) {
            return 0;
        }  
        
        int start = pages[0], end = 0;
        for (int i = 0; i < pages.length; i++) {
            end = end + pages[i];
            if (pages[i] < start) {
                start = pages[i];
            }
        }
        
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (copy(pages, mid, k)) {
                end = mid;
            } else {
                start = mid;
            }
        }
        
        if (copy(pages, start, k)) {
            return start;
        }
        
        return end;
    }
    
    private boolean copy (int[] pages, int time, int k) {
        int timeSum = 0, person = 0;
        
        for (int i = 0; i < pages.length; i++) {
            if (pages[i] > time) {
                return false;
            }
            
            
            timeSum = timeSum + pages[i];
            
            if (timeSum > time) {
                person++;
                timeSum = pages[i];
            //1. Carefully when discussing `=`, `=` is very likely to be an edge case
            } else if (timeSum == time) {
                person++;
                timeSum = 0;
            }
        }

        //2. This is a `=` case, carefully considering it. 
        if (timeSum != 0) {
            person++;
        }
        
        // Notation: the code below can be similarize to `return k < person`
        if (k < person) {
            return false;
        }
        
        return true;
    }
}
```
# Time complexity
O(nlogn)

# Notes and Tips
1. the code below can be similarize to `return k < person`

```java
if (k < person) {
            return false;
        }
        
        return true;
```

2. Be careful when discussing `=`
