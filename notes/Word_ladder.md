# Algoritm

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
import javafx.util.Pair;

class Solution {

  private int L;
  private HashMap<String, ArrayList<String>> allComboDict;

  Solution() {
    this.L = 0;

    // Dictionary to hold combination of words that can be formed,
    // from any given word. By changing one letter at a time.
    this.allComboDict = new HashMap<String, ArrayList<String>>();
  }

  private int visitWordNode(
      Queue<Pair<String, Integer>> Q,
      HashMap<String, Integer> visited,
      HashMap<String, Integer> othersVisited) {
    Pair<String, Integer> node = Q.remove();
    String word = node.getKey();
    int level = node.getValue();

    for (int i = 0; i < this.L; i++) {

      // Intermediate words for current word
      String newWord = word.substring(0, i) + '*' + word.substring(i + 1, L);

      // Next states are all the words which share the same intermediate state.
      for (String adjacentWord : this.allComboDict.getOrDefault(newWord, new ArrayList<String>())) {
        // If at any point if we find what we are looking for
        // i.e. the end word - we can return with the answer.
        if (othersVisited.containsKey(adjacentWord)) {
          return level + othersVisited.get(adjacentWord);
        }

        if (!visited.containsKey(adjacentWord)) {

          // Save the level as the value of the dictionary, to save number of hops.
          visited.put(adjacentWord, level + 1);
          Q.add(new Pair(adjacentWord, level + 1));
        }
      }
    }
    return -1;
  }

  public int ladderLength(String beginWord, String endWord, List<String> wordList) {

    if (!wordList.contains(endWord)) {
      return 0;
    }

    // Since all words are of same length.
    this.L = beginWord.length();

    wordList.forEach(
        word -> {
          for (int i = 0; i < L; i++) {
            // Key is the generic word
            // Value is a list of words which have the same intermediate generic word.
            String newWord = word.substring(0, i) + '*' + word.substring(i + 1, L);
            ArrayList<String> transformations =
                this.allComboDict.getOrDefault(newWord, new ArrayList<String>());
            transformations.add(word);
            this.allComboDict.put(newWord, transformations);
          }
        });

    // Queues for birdirectional BFS
    // BFS starting from beginWord
    Queue<Pair<String, Integer>> Q_begin = new LinkedList<Pair<String, Integer>>();
    // BFS starting from endWord
    Queue<Pair<String, Integer>> Q_end = new LinkedList<Pair<String, Integer>>();
    Q_begin.add(new Pair(beginWord, 1));
    Q_end.add(new Pair(endWord, 1));

    // Visited to make sure we don't repeat processing same word.
    HashMap<String, Integer> visitedBegin = new HashMap<String, Integer>();
    HashMap<String, Integer> visitedEnd = new HashMap<String, Integer>();
    visitedBegin.put(beginWord, 1);
    visitedEnd.put(endWord, 1);

    while (!Q_begin.isEmpty() && !Q_end.isEmpty()) {

      // One hop from begin word
      int ans = visitWordNode(Q_begin, visitedBegin, visitedEnd);
      if (ans > -1) {
        return ans;
      }

      // One hop from end word
      ans = visitWordNode(Q_end, visitedEnd, visitedBegin);
      if (ans > -1) {
        return ans;
      }
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



# Notes and Tips