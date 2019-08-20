# Algorithm

Two Pointers + divide conquer

# Better solution

Currently Best

## Performance:

Total runtime 1976 ms

Your submission beats 83.60% Submissions!

## Time spent

27 min 

## Times of Wrong answer:

None

## Solution

```java
public class Solution {
    /**
     * @param colors: A list of integer
     * @param k: An integer
     * @return: nothing
     */
    public void sortColors2(int[] colors, int k) {
        // write your code here
        if (colors == null || colors.length == 0) {
            return;
        }
        helper(colors, 0, colors.length -  1, 1, k);
    }
    
    private void helper(int[] colors, int sta, int en, int colorStart, int colorEnd) {
        if (colorStart == colorEnd) {
            return;
        }
        
        if (en <= sta) {
            return;
        }
        
        int colorMed = (colorStart + colorEnd) / 2;
        int start = sta, end = en;
        while (start < end) {
            while (start < end && colors[start] <= colorMed) {
                start++;
            }
            
            while (start < end && colors[end] > colorMed) {
                end--;
            }
            
            if (colors[start] > colors[end]) {
                //System.out.println(start);
                int temp = colors[start];
                colors[start] = colors[end];
                colors[end] = temp;
                start++;
                end--;
            }
        }
        
        if (start == end && colors[start] <= colorMed) {
            start++;
        }
        
        if (start == end && colors[start] > colorMed) {
            end--;
        }
        
        helper(colors, sta, end, colorStart, colorMed);
        helper(colors, start, en, colorMed + 1, colorEnd);
    }
}
```

# Time complexity

O(nlogk)

# Notes and Tips

