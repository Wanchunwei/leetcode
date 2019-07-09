# Algorism 

BFS

# Better solution 

Union find

# Solution 

## Performans:

Runtime: 3 ms, faster than 50.20% of Java online submissions for Graph Valid Tree.

Memory Usage: 44.3 MB, less than 57.24% of Java online submissions for Graph Valid Tree.

## Time spent:

Not Done

## Times of Wrong answer:

1 - Bug 1

```java
class Solution {
    public boolean validTree(int n, int[][] edges) {
        //Bug 1: To solve this problem, first think about the sufficient condition for a Tree: 1. edges = n - 1 2. No node is isolated.  
        if (edges == null || edges.length != n - 1 || n == 0) {
            return false;
        }
        
        Map<Integer, Set<Integer>> graph = Initialize(n, edges);
        //Notation 1: Queue is implemented using LinkeddList.
        Queue<Integer> queue = new LinkedList<>();
        //Notation 2: Set is implemented using HashSet.
        Set<Integer> set = new HashSet<>();
        
        queue.offer(0);
        //Notation 3: Remember to add 0 to set;
        set.add(0);
        while (!queue.isEmpty()) {
            int node = queue.poll();
            for (Integer neibour : graph.get(node)) {
                if (set.contains(neibour)) {
                    continue;
                }
                
                set.add(neibour);
                queue.offer(neibour);
            }
    
        }
        
        return (set.size() == n);
    }
    
    private Map<Integer, Set<Integer>> Initialize(int n, int[][] edges) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        int length = edges.length;
        for (int i = 0; i < n; i++) {
            //Notation 5: HashMap uses put to add an element.  
            graph.put(i, new HashSet<Integer>());
        }
        
        for (int i = 0; i < length; i++) {
            graph.get(edges[i][0]).add(edges[i][1]);
            graph.get(edges[i][1]).add(edges[i][0]);
        }
        
        return graph;
    }
}
```
# Time complexity
O(n)

# Notes and Tips
1. `Map` implemented with `HashMap()`, `Set` implemented with `HashSet()`, `Queue` implemented with `LinkedList()`,   
2. HashMap uses `put` method to add an element. 