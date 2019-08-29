# Algorithm

Dynamic Programming

# Better solution

 Manacher's Algorithm

```java
class Solution {
    public int countSubstrings(String S) {
        char[] A = new char[2 * S.length() + 3];
        A[0] = '@';
        A[1] = '#';
        A[A.length - 1] = '$';
        int t = 2;
        for (char c: S.toCharArray()) {
            A[t++] = c;
            A[t++] = '#';
        }

        int[] Z = new int[A.length];
        int center = 0, right = 0;
        for (int i = 1; i < Z.length - 1; ++i) {
            if (i < right)
                Z[i] = Math.min(right - i, Z[2 * center - i]);
            while (A[i + Z[i] + 1] == A[i - Z[i] - 1])
                Z[i]++;
            if (i + Z[i] > right) {
                center = i;
                right = i + Z[i];
            }
        }
        int ans = 0;
        for (int v: Z) ans += (v + 1) / 2;
        return ans;
    }
}
```



## Performance:

Runtime: 6 ms, faster than 38.28% of Java online submissions for Palindromic Substrings.

Memory Usage: 35.7 MB, less than 68.36% of Java online submissions for Palindromic Substrings.

## Time spent:

10 min 

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    public int countSubstrings(String s) {
        boolean[][] isPalindromic = new boolean[s.length()][s.length()];
        int count = 0;
        for (int i = 0; i < s.length(); i++) {
            isPalindromic[i][i] = true;
            if (i != s.length() - 1 && s.charAt(i) == s.charAt(i + 1)) {
                isPalindromic[i][i + 1] = true;
            } 
        }
        
        for (int i = s.length() - 1; i >= 0; i--) {
            for (int j = i; j < s.length(); j++) {
                if (s.charAt(i) == s.charAt(j) && (i + 1 >= j - 1 || isPalindromic[i + 1][j - 1])) {
                    isPalindromic[i][j] = true;
                }
            }
        }
        
        for (int i = 0; i < s.length(); i++) {
            for (int j = i; j < s.length(); j++) {
                if (isPalindromic[i][j]) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

# Time complexity

O(n^2)

# Notes and Tips

