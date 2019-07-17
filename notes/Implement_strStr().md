# Algorithm 

Rabin Karp

# Better solution 

KMP

# Solution

Runtime: 3 ms, faster than 45.29% of Java online submissions for Implement strStr().

Memory Usage: 36.9 MB, less than 99.96% of Java online submissions for Implement strStr().

```java
class Solution {
    private static int BASE = 1000000;
    public int strStr(String haystack, String needle) {
       /*
         Coding Style Notation: 
         1.Check whether the given string is null.
         2.Check wehther the given string is empty. 
        */
        if(haystack == null || needle == null){
            return -1;
        }
        
        int length = needle.length();
        
        if(length == 0){
            return 0;
        }
        
        //Caculate power(31, m)
        int power = 1;
        for (int i = 0; i < length; i++) {
            power = (power * 31) % BASE;
        }
        
        //Caculate hashcode of needle
        int needleCode = 0;
        for (int i = 0; i < length; i++) {
            needleCode = (needleCode * 31 + needle.charAt(i)) % BASE;
        }
        
        //Hashcode of substring of haystack
        int hashcode = 0;
        for (int i = 0; i < haystack.length(); i++) {
            hashcode = (hashcode * 31 + haystack.charAt(i)) % BASE;
            
            if (i < length - 1) {
                continue;
            }
            
            if (i >= length) {
                hashcode = hashcode - (haystack.charAt(i - length) * power) % BASE;
                if (hashcode < 0) {
                    hashcode = hashcode + BASE;
                }
            }
            
            if (hashcode == needleCode) {
                if (needle.equals(haystack.substring(i - length + 1, i + 1))) {
                    return i - length + 1;
                }
            }
        }
        
        return -1;
    }
}
```

# Time complexity

O(n + m)

# Notes and Tips

1. When generating hashcode and power, take care of that number may be too large and exceed. So we should do mod after mutiplying every time.

```java
        for (int i = 0; i < length; i++) {
            power = (power * 31) % BASE;
        }
```

2. Be attention to here. We must check whether the hashcode is negative;

```java
        hashcode = hashcode - (haystack.charAt(i - length) * power) % BASE;
        if (hashcode < 0) {
            hashcode = hashcode + BASE;
        }
```

# Question type and Relavent Question

- String

