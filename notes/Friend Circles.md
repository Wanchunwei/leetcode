# Algorithm 

BFS

# Better solution 

Currently Best
    
other solution : DFS(faster but not recommended because stack overflow and BFS is clearer and simpler)

More concise solution for BFS : 

```java
public class Solution {
    public int findCircleNum(int[][] M) {
        int[] visited = new int[M.length];
        int count = 0;
        Queue < Integer > queue = new LinkedList < > ();
        for (int i = 0; i < M.length; i++) {
            if (visited[i] == 0) {
                queue.add(i);
                while (!queue.isEmpty()) {
                    int s = queue.remove();
                    visited[s] = 1;
                    for (int j = 0; j < M.length; j++) {
                        if (M[s][j] == 1 && visited[j] == 0)
                            queue.add(j);
                    }
                }
                count++;
            }
        }
        return count;
    }
}
```



## Performance:

Runtime: 5 ms, faster than 26.85% of Java online submissions for Friend Circles.

Memory Usage: 45.9 MB, less than 36.00% of Java online submissions for Friend Circles.

## Time spent:

17 min 5 seconds'

## Times of Wrong answer:

2 - Bug 1, Bug 2

## Solution

```java
class Solution {
    public int findCircleNum(int[][] M) {
        if (M == null || M.length == 0 || M[0].length == 0) {
            return 0;
        }
        
        List<Integer>[] relation = new List[M.length];
        for (int i = 0; i < M.length; i++) {
            relation[i] = new ArrayList<Integer>();
            for (int j = 0; j < M.length; j++) {
                if (i != j && M[i][j] == 1) {
                    relation[i].add(j);
                }
            }
        }
        
        int count = 0;
        int[] students = new int[M.length];
        for (int i = 0; i < M.length; i++) {
            students[i]++;
        }
        
        Set<Integer> set = new HashSet<>();
        while (set.size() != M.length) {
            Queue<Integer> queue = new LinkedList<>();
            for (int i = 0; i < M.length; i++) {
                if (students[i] == 1) {
                    queue.offer(i);
                    set.add(i);
                    students[i]--;
                    break;
                }
            }
            
            while (!queue.isEmpty()) {
                int student = queue.poll();
                for (Integer friend : relation[student]) {
                    if (!set.contains(friend)) {
                        set.add(friend);
                        queue.offer(friend);
                        students[friend]--;
                    }
                }
            }
            
            count++;
        }
        
        return count;
    }
}
```

# Time complexity

O(V + E)

# Notes and Tips

