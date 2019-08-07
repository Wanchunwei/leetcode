# Algorithm 

DFS + BFS



Analysis : 

1. First applying BFS to find the minimum distance between `beginWord` and `endWord`. ---- (Word Ladder Solved), to avoid time exceed, we also record the distance for each node to `endWord` 
2. Apply DFS to find all the paths that from `beginWord` to `endWord`,  the distance  between which is minimum distance.

# Better solution

Currently Best

## Performance:

Runtime: 112 ms, faster than 46.21% of Java online submissions for Word Ladder II.

Memory Usage: 56.9 MB, less than 8.75% of Java online submissions for Word Ladder II.

## Time spent:

Not Done

## Times of Wrong answer:

2 - Bug 1, Bug 2

# Solution 

```java
class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        List<List<String>> results = new ArrayList<>();
        List<String> temp = new ArrayList<>();
        
        if (wordList == null || !wordList.contains(endWord)) {
            return results;
        }
        
        Map<String, List<String>> map = new HashMap<>();

        //Notation : Remember to add beginWord to map.
        for (int i = 0; i < beginWord.length(); i++) {
            String s = beginWord.substring(0, i) + "*" + 
                       beginWord.substring(i + 1, beginWord.length());
            if (!map.containsKey(s)) {
                map.put(s, new ArrayList<String>());
            }
            map.get(s).add(beginWord);
        }
        
        for (int i = 0; i < wordList.size(); i++) {
            for (int j = 0; j < wordList.get(i).length(); j++) {
                String neighbor = wordList.get(i).substring(0, j) + "*" + 
                                  wordList.get(i).substring(j + 1, wordList.get(i).length());
                if (!map.containsKey(neighbor)) {
                    map.put(neighbor, new ArrayList<String>());
                }
                map.get(neighbor).add(wordList.get(i));
            }
        }
        
        Map<String, Integer> distance = bfs(wordList, map, beginWord, endWord);
        //Notation : Before use get method of Map, remember to make sure this is not a null
        if (distance.get(beginWord) == null) {
            return results;
        }
        int min = distance.get(beginWord);
        dfs(beginWord, endWord, wordList, distance, results, temp, min - 1, map);
        
        List<List<String>> paths = new ArrayList<>();
        for (List<String> list : results) {
            List<String> path = new ArrayList<>();
            if (!list.contains(beginWord)) {
                path.add(beginWord);  
            }
            for (String s : list) {
                path.add(s);
            }
            
            paths.add(path);
        }
        
        return paths;
    }
    
    private void dfs(String beginWord, 
                     String endWord, 
                     List<String> wordList,
                     Map<String, Integer> distance,
                     List<List<String>> results,
                     List<String> temp,
                     int min,
                     Map<String, List<String>> map) {
        if (min == 0 && isNeighbor(beginWord, endWord, map)) {
            temp.add(endWord);
            results.add(new ArrayList<String>(temp));
            temp.remove(temp.size() - 1);
            return;
        }
    
        
        for (int i = 0; i < wordList.size(); i++) {
            //Notation : Before use get method of Map, remember to make sure this is not a null
            if (distance.get(wordList.get(i)) == null) {
                continue;
            }
            
            if (distance.get(wordList.get(i)) == min 
                && isNeighbor(beginWord, wordList.get(i), map)) {
                temp.add(wordList.get(i));
                dfs(wordList.get(i), endWord, wordList, distance, results, temp, min - 1, map);
                temp.remove(temp.size() - 1);
            }
        }
    }
    
    private boolean isNeighbor(String beginWord, 
                               String neighbor, 
                               Map<String, List<String>> map) {
        for (int i = 0; i < beginWord.length(); i++) {
            String s = beginWord.substring(0, i) + "*" + 
                       beginWord.substring(i + 1, beginWord.length());
            if (map.get(s).contains(neighbor)) {
                return true;
            }
        }
        
        return false;
    }
    
    private Map<String, Integer> bfs(List<String> wordList, 
                                     Map<String, List<String>> map, 
                                     String beginWord, 
                                     String endWord) {
        Map<String, Integer> distance = new HashMap<>();
        Queue<String> queue = new LinkedList<>();
        Set<String> set = new HashSet<>();
        int level = 1;
        
        queue.offer(endWord);
        set.add(endWord);
        distance.put(endWord, 0);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int j = 0; j < size; j++) {
                String str = queue.poll();
                for (int i = 0; i < str.length(); i++) {
                    String s = str.substring(0, i) + "*" + 
                               str.substring(i + 1, str.length());
                    for (String neighbor : map.get(s)) {
                        if (!set.contains(neighbor)) {
                            queue.offer(neighbor);
                            distance.put(neighbor, level);
                            //Bug2 : Remember to add set.add();
                            set.add(neighbor);
                        }
                    }
                }
            }
            level++;
        }
        
        return distance;
    }
}
```

# Time complexity

O(N * N * L) --- N is the number of word, L is the length of a word.  

# Note and tips

1. Before use get method of `Map`, remember to make sure the value is not null