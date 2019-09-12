# Algorithm

Two pointers

# Better solution

Currently Best

## Performance:

Runtime: 3 ms, faster than 80.64% of Java online submissions for Longest Substring with At Most K Distinct Characters.

Memory Usage: 36.4 MB, less than 100.00% of Java online submissions for Longest Substring with At Most K Distinct Characters.

## Time spent:

15 min

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        
        int[] count = new int[256];
        int start = 0, end = 0, num = 0, max = 0;
        while (end < s.length()) {
            if (count[s.charAt(end)] == 0) {
                num++;
            }
            count[s.charAt(end)]++;
            if (num <= k) {
                max = Math.max(max, end - start + 1);
            } else {
                while (num > k) {
                    count[s.charAt(start)]--;
                    if (count[s.charAt(start)] == 0) {
                        num--;
                    }
                    start++;
                }
            }
            end++;
        }
        
        return max;
    }
}
```



# Time complexity

O(n)

# Notes and Tips

