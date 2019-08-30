# Algorithm

Union Find

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 100.00% of Java online submissions for Satisfiability of Equality Equations.

Memory Usage: 36.1 MB, less than 100.00% of Java online submissions for Satisfiability of Equality Equations.

## Time spent:

21 min 37 seconds 

## Times of Wrong answer:

2 - Bug 1, Bug 2

## Solution

```java
class Solution {
    public boolean equationsPossible(String[] equations) {
        char[] father = new char[26];
        for (int i = 0; i < equations.length; i++) {
            if (equations[i].charAt(0) == equations[i].charAt(3) && equations[i].charAt(1) == '!') {
                return false;
            }
            
            if (equations[i].charAt(1) == '=') {
                if ((int)father[equations[i].charAt(0) - 'a'] == 0) {
                    father[equations[i].charAt(0) - 'a'] = equations[i].charAt(0);
                }
                
                if ((int)father[equations[i].charAt(3) - 'a'] == 0) {
                    father[equations[i].charAt(3) - 'a'] = equations[i].charAt(3);
                }
                
                connect(father, equations[i].charAt(0), equations[i].charAt(3));
            }
        }
        
        for (int i = 0; i < equations.length; i++) {
            //Bug 1 : Corner case that if the character is not initiated in father array  
            if (equations[i].charAt(1) == '!' && 
                (int)father[equations[i].charAt(0) - 'a'] != 0 &&
                (int)father[equations[i].charAt(3) - 'a'] != 0 &&
                find(father, equations[i].charAt(0)) == find(father, equations[i].charAt(3))) {
                return false;
            }
        }
        
        return true;
    }
    
    private void connect(char[] father, char c1, char c2) {
        char fatherC1 = find(father, c1);
        char fatherC2 = find(father, c2);
        if (fatherC1 != fatherC2) {
            father[fatherC1 - 'a'] = fatherC2;
        }
        return;
    }
    
    private char find(char[] father, char c) {
        if (father[c - 'a'] == c) {
            return c;
        }
        
        return father[c - 'a'] = find(father, father[c - 'a']);
    }
}
```

# Time complexity

O(n)

# Notes and Tips

1.  Corner case that if the character is not initiated in father array  