# Algorithm

DFS + Memory

# Better solution

Currently Best

## Performance:

Runtime: 7 ms, faster than 52.67% of Java online submissions for Word Break II.

Memory Usage: 39.3 MB, less than 34.43% of Java online submissions for Word Break II.

## Time spent

Not Done

## Times of Wrong answer:

2

## Solution

```java
class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        Set<String> set = new HashSet<>(wordDict);
        String temp = "";
        Map<Integer, List<String>> map = new HashMap<>();
        return dfs(s, set, map, 0);
    }
    
    private List<String> dfs(String s, 
                     Set<String> set, 
                     Map<Integer, List<String>> map,
                     int start){
        List<String> temp = new ArrayList<>();
        if (map.containsKey(start)) {
            return map.get(start);
        }
        
        for (int i = 0; i < s.length(); i++) {
            if (set.contains(s.substring(0, i + 1))) {
                if (i + 1 == s.length()) {
                    temp.add(s.substring(0, i + 1));
                }
                List<String> wordBreak = dfs(s.substring(i + 1, s.length()), set, map, i + 1 + start);
                for (String str : wordBreak) {
                    temp.add(s.substring(0, i + 1) + " " + str);
                }       
            }
        }
        
        map.put(start, temp);
        return temp;
    }
}
```

# Time complexity

O(n^3)

# Notes and Tips

