# Algorithm

Sweep-Line + Two pointers



Analysis:

1. Using map to store all positions of each unique character in S.

2. Sweep - Line : We using an array `int[] interval`to store the first position and last position for each character in S. 

   i.e. If `S.charAt(i)` is the first position a character appears in S, `interval[i]++`. If `S.charAt(i)`  is the first position a character appears in S, `interval[i]--`.  We can get the first position and last position from `position.get(0)` and `position.get(position.size() - 1)`

3. Two pointers : Go through `int[] interval`, we keep a start position of current interval and a interger `interv`. If `interv == 0`, then the interval is a valid interval that includes both first position and last position of characters in this interval . So we can add the interval to `results`, then let current position be the start position of next valid interval.

# Better solution

Currently Best

## Performance:

Runtime: 8 ms, faster than 15.47% of Java online submissions for Partition Labels.

Memory Usage: 36.1 MB, less than 96.10% of Java online submissions for Partition Labels.

## Time spent:

21 min 

## Times of Wrong answer:

1 - Bug 1

## Solution

```java
class Solution {
    public List<Integer> partitionLabels(String S) {
        List<Integer> results = new ArrayList<>();
        Map<Character, List<Integer>> map = new HashMap<>();
        int[] interval = new int[S.length()];
        for (int i = 0; i < S.length(); i++) {
            if (!map.containsKey(S.charAt(i))) {
                map.put(S.charAt(i), new ArrayList<Integer>());
            }
            map.get(S.charAt(i)).add(i);
        }
        
        for (Character c : map.keySet()) {
            List<Integer> position = map.get(c);
            // Bug 1 : Be careful that if a character only appears in S once, then the position of the character are both first position and last position. So we just let interval[i] ++ then --, so it will be 0. 
            interval[position.get(0)]++;
            interval[position.get(position.size() - 1)]--;
        }
        
        int start = 0, interv = 0;
        for (int i = 0; i < interval.length; i++) {
            if (interval[i] == 1) {
                interv++;
            }
        
            if (interval[i] == -1) {
                interv--;
            }
            
            if (interv == 0) {
                results.add((i - start + 1));
                start = i + 1;
            }
            
        }
        
        return results;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

1. Be careful that if a character only appears in S once, then the position of the character are both first position and last position. So we just let interval[i] ++ then --, so it will be 0. 