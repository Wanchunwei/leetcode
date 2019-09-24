# Algorithm 

DP

# Better solution 

DP with O(nlogn)

```java

```



# Performance

Runtime: 286 ms, faster than 41.62% of Java online submissions for Russian Doll Envelopes.

Memory Usage: 54.3 MB, less than 38.46% of Java online submissions for Russian Doll Envelopes.

# Time spent:

10 min

# Times of Wrong answer:

1 - Bug 1

# Solution 

```java
class Solution {
    public int maxEnvelopes(int[][] envelopes) {
        if (envelopes == null || envelopes.length == 0 || envelopes[0].length == 0) {
            return 0;
        } 
        
        Arrays.sort(envelopes, new Comparator<int[]>() {
            public int compare(int[] a, int[] b) {
                if (a[0] == b[0]) {
                    return a[1] - b[1];
                } else {
                    return a[0] - b[0];
                }
            }
        });
        
        int max = 1;
        int russDoll[] = new int[envelopes.length];
        russDoll[0] = 1;
        for (int i = 1; i < russDoll.length; i++) {
            //Bug 1 : Here we must initialize the russDoll[i] to 1.
            russDoll[i] = 1;
            for (int j = 0; j < i; j++) {
                if (envelopes[j][0] < envelopes[i][0] && 
                    envelopes[j][1] < envelopes[i][1] && 
                    russDoll[j] + 1 > russDoll[i]) {
                    russDoll[i] = russDoll[j] + 1;
                }
            }
            
            max = Math.max(max, russDoll[i]);
        }
        return max;
    }
}
```



# Time complexity

O(n^2)

# Corner cases :

1.  The value of each russDoll[i] should be first initialized with 1;

# Notes and Tips

1. ```java
   //Remember the comparator of Arrays.sort().
   Arrays.sort(envelopes, new Comparator<int[]>() {
               public int compare(int[] a, int[] b) {
                   if (a[0] == b[0]) {
                       return a[1] - b[1];
                   } else {
                       return a[0] - b[0];
                   }
               }
           });
   ```