# Algorithm

BFS (Topological sorting)

## Best Solution:

Union Find

## Performance:

Runtime: 7 ms, faster than 36.45% of Java online submissions for Number of Connected Components in an Undirected Graph.

Memory Usage: 46.2 MB, less than 13.96% of Java online submissions for Number of Connected Components in an Undirected Graph.

## Time spent:

24 min 12 seconds

## Times of Wrong answer:

2 - Bug 1, Bug2

## Solution

```java
class Solution {
    public int countComponents(int n, int[][] edges) {
        if (edges == null || edges.length == 0) {
            return n;
        }
        
        int nums = 0;
        //Bug 1 : Remember to indicate generic when initializing List[],                           otherwise "for (Integer neighbor : graph[current])" can only                     read it as an Object(not integer)
        List<Integer>[] graph = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            graph[i] = new ArrayList<Integer>();
        }
        
        //Bug 2 : Remember to add both nodes to neighbors of each other in                         a undirect graph 
        for (int i = 0; i < edges.length; i++) {
            graph[edges[i][0]].add(edges[i][1]);   
            graph[edges[i][1]].add(edges[i][0]);  
        }
        
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> set = new HashSet<>();
        boolean[] visit = new boolean[n];
        
        while (set.size() != n) {
            int node = findNode(visit);
            if (node == -1) {
                return nums;
            }
            
            queue.offer(node);
            set.add(node);
            visit[node] = true;
            while (!queue.isEmpty()) {
                int current = queue.poll();
                for (Integer neighbor : graph[current]) {
                    if (!set.contains(neighbor)) {
                        queue.offer(neighbor);
                        set.add(neighbor);
                        visit[neighbor] = true;
                    }
                }
            }
            nums++;
        }
        
        return nums;
    }
    
    private int findNode(boolean[] visit) {
        for (int i = 0; i < visit.length; i++) {
            if (visit[i] != true) {
                return i;
            }
        }
        //Bus 3 : Remember to add return statement in a function
        return -1;
    }
}
```



# Time complexity

O(nm)

# Notes and Tips

1. Remember to indicate generic when initializing `List[]`, otherwise `for (Integer neighbor : graph[current])` can only read it as an Object(not integer)
2. Remember to add both nodes to neighbors of each other in a undirect graph
3. Remember to add return statement in a function