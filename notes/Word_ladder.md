# Algorithm

BFS

# Better solution 

BFS (with HashMap) (O(MN)) 

Time Spent : 29 min

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String>                                                                     wordList) {
        if (wordList == null || wordList.size() == 0 ||                                                         !wordList.contains(endWord)) {            
            return 0;
        }
        
        Map<String, ArrayList<String>> map = new HashMap<>();
        for (int i = 0; i < wordList.size(); i++) {
            for (int j = 0; j < wordList.get(i).length(); j++) {
                String newWord = wordList.get(i).substring(0, j) + "*" +                                          wordList.get(i).substring(j + 1,                                                wordList.get(i).length());
                if (map.containsKey(newWord)) {
                    ArrayList<String> neighbor = map.get(newWord);
                    neighbor.add(wordList.get(i));
                    map.put(newWord, neighbor);
                } else {
                    ArrayList<String> neighbor = new ArrayList<String>();
                    neighbor.add(wordList.get(i));
                    map.put(newWord, neighbor);
                }
            }
        }
        
        Queue<String> queue = new LinkedList<>();
        Set<String> set = new HashSet<>();
        int level = 1;
        
        queue.offer(beginWord);
        set.add(beginWord);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int j = 0; j < size; j++) {
                String node = queue.poll();
                for (int i = 0; i < node.length(); i++) {
                    String mapWord =  node.substring(0, i) + "*" +                                                     node.substring(i + 1, node.length());
                    if (!map.containsKey(mapWord)) {
                    	continue;
                	}
                
                	for (String neighbor : map.get(mapWord)) {
                    	if (neighbor.equals(endWord)) {
                        	return ++level;
                   		}
                    
                    	if (!set.contains(neighbor)) {
                        	queue.offer(neighbor);
                        	set.add(neighbor);
                    	}
                	}
            	}
          	}
            level++;
        }
        
        return 0;
    }
}
```

# Best Solution:

Bidirection BFS (O(MN))

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> 																	  wordList) {
        if (wordList == null || wordList.size() == 0 || 									!wordList.contains(endWord)) {
            return 0;
        }
        
        Map<String, ArrayList<String>> map = new HashMap<>();
        for (int i = 0; i < wordList.size(); i++) {
            for (int j = 0; j < wordList.get(i).length(); j++) {
                String newWord = wordList.get(i).substring(0, j) + "*" +                                          wordList.get(i).substring(j + 1, 												 wordList.get(i).length());
                if (map.containsKey(newWord)) {
                    ArrayList<String> neighbor = map.get(newWord);
                    neighbor.add(wordList.get(i));
                    map.put(newWord, neighbor);
                } else {
                    ArrayList<String> neighbor = new ArrayList<String>();
                    neighbor.add(wordList.get(i));
                    map.put(newWord, neighbor);
                }
            }
        }
        
        Queue<String> queueBegin = new LinkedList<>();
        Queue<String> queueEnd = new LinkedList<>();
        Set<String> setBegin = new HashSet<>();
        Set<String> setEnd = new HashSet<>();
        
        int level = 2;

        
        queueBegin.offer(beginWord);
        setBegin.add(beginWord);
        queueEnd.offer(endWord);
        setEnd.add(endWord);
        
        Queue<String> queue = null;
        Set<String> setCur = null, setOp = null;
        while (!queueBegin.isEmpty() && !queueEnd.isEmpty()) {
            //Notation : Create reference collections to refer when doing                                bidirection BFS 
            if (queueBegin.size() <= queueEnd.size()) {
                queue = queueBegin;
                setCur = setBegin;
                setOp = setEnd;
            } else {
                queue = queueEnd;
                setCur = setEnd;
                setOp = setBegin;
            }
            
            int size = queue.size();
            for (int j = 0; j < size; j++) {
            	String node = queue.poll();
           	 	for (int i = 0; i < node.length(); i++) {
                	String mapWord =  node.substring(0, i) + "*" +                                                     node.substring(i + 1, node.length());
                	if (!map.containsKey(mapWord)) {
                    	continue;
                	}
                
                	for (String neighbor : map.get(mapWord)) {
                    	if (setOp.contains(neighbor)) {
                        	return level;
                    	}
                    
                    	if (!setCur.contains(neighbor)) {
                        	queue.offer(neighbor);
                        	setCur.add(neighbor);
                    	}
                	}
            	}
          }
          level++;
        }
        
        return 0;
    }
}
```



## Performance:

Runtime: 836 ms, faster than 6.15% of Java online submissions for Word Ladder.

Memory Usage: 39.9 MB, less than 83.75% of Java online submissions for Word Ladder.

## Time spent:

19 min 23 seconds

## Times of Wrong answer:

None

## Solution

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        int length = 1;
        if (!wordList.contains(endWord)) {
            return 0;
        }
        
        Queue<String> queue = new LinkedList<>();
        Set<String> set = new HashSet<>();
        queue.offer(beginWord);
        set.add(beginWord);
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String temp = queue.poll();
                for (int j = 0; j < wordList.size(); j++) {
                    if (canTransform(temp, wordList.get(j)) &&                                                         (wordList.get(j).equals(endWord))) {
                        return ++length;
                    }
                    
                    if (canTransform(temp, wordList.get(j)) && 
                        !set.contains(wordList.get(j))) {
                        queue.offer(wordList.get(j));
                        set.add(wordList.get(j));
                    }
                }
            }
            
            length++;
        }
        
        return 0;
    }
    
    private boolean canTransform(String temp, String target) {
        int count = 0;
        for (int i = 0; i < temp.length(); i++) {
            if (temp.charAt(i) != target.charAt(i)) {
                count++;
            }
        }
        
        return (count == 1);
    }
}
```

# Time complexity

O(MN^2)

# Notes and Tips

1. `substring(start, end)` method 

   returns `substring[start, end)` if `start < end`

   returns `""` if `start == end`, 

   returns `substring(end, start)` if  `start > end`

2. `Map.getOrDefault(key, value)` method (JDK 8 new method)

   returns `Map.get(key)`if `Map.contains(key)`

   returns `value` if `!Map.contains(key)`

3. `Set<>, Queue<> and List<> are Objects that can be references`

