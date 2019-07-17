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

Runtime: 4 ms, faster than 81.55% of Java online submissions for Course Schedule II.

Memory Usage: 44.9 MB, less than 91.37% of Java online submissions for Course Schedule II.

## Time spent:

22 min 05 seconds

## Times of Wrong answer:

4 - Bug 1, Bug 2

## Solution
```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        int count = 0;
        //Notation1 : when initializing an Array, all the space allocated wil be initialized with 0;
        int[] order = new int[numCourses];
        if (numCourses == 0) {
            //Notation2 :  when initializing an Array, we must initialize it with a size. 
            return new int[0];
        }
        
        int[] indegree = new int[numCourses];
        List[] subCourses = new ArrayList[numCourses];
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> set = new HashSet<>();
        
        for (int i = 0; i < numCourses; i++) {
            subCourses[i] = new ArrayList<Integer>();
        }
        
        for (int i = 0; i < prerequisites.length; i++) {
            indegree[prerequisites[i][0]]++;
            subCourses[prerequisites[i][1]].add(prerequisites[i][0]);
        }
        
        for (int i = 0; i < numCourses; i++) {
            if (indegree[i] == 0) {
                queue.offer(i);
            }
        }
        
        while (!queue.isEmpty()) {
            int course = queue.poll();
            set.add(course);
            order[count] = course;
            for (int i = 0; i < subCourses[course].size(); i++) {
                indegree[(int)subCourses[course].get(i)]--;
                if (indegree[(int)subCourses[course].get(i)] == 0) {
                    queue.offer((int)subCourses[course].get(i));
                }
            }
            //Bug : Remember to count++
            count++;
        }
        
        //Bug : We need a set to judge whether given nodes can be topological sort. 
        if (set.size() == numCourses) {
            return order;
        }

        return new int[0];
    }
}
```
# Time complexity
O(V + E)

# Notes and Tips
1. when initializing an `Array`, we must initialize it with a `size` and all the space allocated wil be initialized with 0;
2. A `set` can be used to judge whether given nodes can be topological sort. 
