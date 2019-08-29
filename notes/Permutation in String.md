# Algorithm

Two pointers

# Better solution

Currently Best

## Performance:

Runtime: 5 ms, faster than 84.03% of Java online submissions for Permutation in String.

Memory Usage: 37.4 MB, less than 88.46% of Java online submissions for Permutation in String.

## Time spent:

19 min 

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        if (s2.length() < s1.length()) {
            return false;
        }
        
        int[] nums = new int[26];
        int counter = s1.length(), start = 0, end = 0;
        for (int i = 0; i < s1.length(); i++) {
            nums[s1.charAt(i) - 'a']++;
        }
        
        while (end < s2.length()) {
            if (end < s1.length()) {
                nums[s2.charAt(end) - 'a']--;
                if (nums[s2.charAt(end) - 'a'] >= 0) {
                    counter--;
                }
                end++;
                continue;
            }
            
            if (counter == 0) {
                return true;
            }
            
            nums[s2.charAt(start) - 'a']++;
            if (nums[s2.charAt(start) - 'a'] > 0) {
                counter++;
            }
            
            nums[s2.charAt(end) - 'a']--;
            if (nums[s2.charAt(end) - 'a'] >= 0) {
                counter--;
            }
            
            start++;
            end++;
        }
        
        if (counter == 0) {
            return true;
        }
        
        return false;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

