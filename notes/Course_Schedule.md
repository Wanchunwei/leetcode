# Algorithm 

BFS (Topological Sorting)

Analysis: 
1. Get indegree of all nodes by traversing all nodes and its neighbors in the given ArrayList. - `getIndegree()`
2. Create edges array for each node. - `getSubCourses()`
3. Find start nodes for whose indegree is 0. `getStartNodes()`
4. From a start node, BFS all nodes, if degree becomes 0, add to array. `bfs()` 

# Better solution 

Currently Best
    
other solution : DFS

## Performans:

Runtime: 7 ms, faster than 56.70% of Java online submissions for Course Schedule.

Memory Usage: 44.9 MB, less than 86.14% of Java online submissions for Course Schedule.

## Time spent:

Not Done

## Times of Wrong answer:

2 - Bug 1, Bug 2

## Solution
```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (numCourses == 0 || prerequisites == null || prerequisites.length == 0) {
            return true;
        }
        
        ArrayList<Integer> indegree = getIndegree(numCourses, prerequisites);
        ArrayList<ArrayList<Integer>> subCourses = getSubCourses(numCourses, prerequisites);
        ArrayList<Integer> startCourses = getStartCourses(indegree);
        boolean isFnished = bfs(numCourses, subCourses, startCourses, indegree);
        
        return isFnished;
    }
    
    private ArrayList<Integer> getIndegree(int numCourses, int[][] prerequisites) {
        ArrayList<Integer> indegree = new ArrayList<Integer>(numCourses);
        for (int i = 0; i < numCourses; i++) {
            //Bug 1 : `ArrayList` must use `set(index, value)` to change value rather than`get.(index) = value`.
            //Bug 2 : `ArrayList<>(n)` is not initialized with size of n but only capacity of n, so that you cannot directly use `set(inex. value)` but first `add(value)`
            indegree.add(0);
        }
        
        for (int i = 0; i < prerequisites.length; i++) {
            indegree.set(prerequisites[i][1], indegree.get(prerequisites[i][1]) + 1);
        }
        
        return indegree;
    }
    
    private ArrayList<ArrayList<Integer>> getSubCourses(int numCourses, 
                                                        int[][] prerequisites) {
        ArrayList<ArrayList<Integer>> subCourses = new ArrayList<>(numCourses);
        //Notation 1 : Remember to initialize ArrayList. 
        for (int i = 0; i < numCourses; i++) {
            subCourses.add(new ArrayList<Integer>());
        }
        
        for (int i = 0; i < prerequisites.length; i++) {
            subCourses.get(prerequisites[i][0]).add(prerequisites[i][1]);
        }
        
        return subCourses;
    }
    
    private ArrayList<Integer> getStartCourses(ArrayList<Integer> indegree) {
        ArrayList<Integer> startCourses = new ArrayList<Integer>();
        for (int i = 0; i < indegree.size(); i++) {
            if (indegree.get(i) == 0) {
                startCourses.add(i);
            }
        }
        
        return startCourses;
    }
    
    private boolean bfs(int numCourses, 
                        ArrayList<ArrayList<Integer>> subCourses, 
                        ArrayList<Integer> startCourses, 
                        ArrayList<Integer> indegree) {
        Set<Integer> set = new HashSet<>();
        Queue<Integer> queue = new LinkedList<>();
        
        for (int i = 0; i < startCourses.size(); i++) {
            queue.offer(startCourses.get(i));
        }
        
        while (!queue.isEmpty()) {
            int course = queue.poll();
            set.add(course);
            for (int j = 0; j < subCourses.get(course).size(); j++) {
                indegree.set(subCourses.get(course).get(j), indegree.get(subCourses.get(course).get(j)) - 1);
                if (indegree.get(subCourses.get(course).get(j)) == 0) {
                    queue.offer(subCourses.get(course).get(j));
                }
            }
        }
        
        return (set.size() == numCourses);
            
    }
}
```
# Time complexity
O(V + E)

# Notes and Tips
1. `ArrayList` must use `set(index, value)` to change value rather than`get.(index) = value`.
2. `ArrayList<>(n)` is not initialized with size of n but only capacity of n, so that you cannot directly use `set(index. value)` without initializing index. Here should first `add(value)`.
