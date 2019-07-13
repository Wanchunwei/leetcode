# Algorithm 

BFS

Analysis: 
1. Get indegree of all nodes by traversing all nodes and its neighbors in the given ArrayList. - `getIndegree()`
2. Find start nodes for whose indegree is 0. `getStartNodes()`
3. From a start node, BFS all nodes, if degree becomes 0, add to array. `bfs()` 

# Better solution 

Currently Best
    
other solution : DFS(not recommended because BFS is clearer and simpler)

## Performance:

Total runtime: 3204ms

## Time spent:

54 min

## Times of Wrong answer:

2 - Bug 1, Bug 2

## Solution
```java
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     ArrayList<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) { label = x; neighbors = new ArrayList<DirectedGraphNode>(); }
 * };
 */

public class Solution {
    /*
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        // write your code here
        ArrayList<DirectedGraphNode> results = new ArrayList<>();
        
        //Bug 1: For normal array like String[], we can use String[].length, but for             ArrayList we must use size().
        if (graph.size() == 0 || graph == null) {
            return results;
        }

        Map<DirectedGraphNode, Integer> indegree = getIndegree(graph);
        ArrayList<DirectedGraphNode> startNodes = getStartNodes(indegree);
        results = bfs(startNodes, indegree);
        
        return results;
    }
    
    private Map<DirectedGraphNode, Integer> getIndegree (ArrayList<DirectedGraphNode> graph) {
        Queue<DirectedGraphNode> queue = new LinkedList<>();
        Set<DirectedGraphNode> set = new HashSet<>();
        Map<DirectedGraphNode, Integer> indegree = new HashMap<>();
        
        for (DirectedGraphNode node : graph) {
            // Bug 2: We must gurantee that the node is not added to our set 
            if (!set.contains(node)) {
                indegree.put(node, 0);
                set.add(node);
            }
            
            for (DirectedGraphNode neighbor : node.neighbors) {
                if (!set.contains(neighbor)) {
                    queue.offer(neighbor);
                    set.add(neighbor);
                    indegree.put(neighbor, 1);
                } else {
                    //Notation : In java, we can not directly change the value of                               HashMap. To acheive this, We must reinsert the pair with the same                         key value.
                    indegree.put(neighbor, indegree.get(neighbor) + 1);
                }
            }
        }
        
        return indegree;
    }
    
    private ArrayList<DirectedGraphNode> getStartNodes(Map<DirectedGraphNode, Integer> indegree){
        ArrayList<DirectedGraphNode> startNodes = new ArrayList<>();
        //Notation 2: To traverse a Map, we can traverse its keySet. 
        for (DirectedGraphNode node : indegree.keySet()) {
            if (indegree.get(node) == 0) {
                startNodes.add(node);
            }
        }
        return startNodes;
    }
    
    private ArrayList<DirectedGraphNode> bfs (ArrayList<DirectedGraphNode> startNodes,
                                              Map<DirectedGraphNode, Integer> indegree) {
                                                  
        ArrayList<DirectedGraphNode> results = new ArrayList<>();
        Queue<DirectedGraphNode> queue = new LinkedList<DirectedGraphNode>();
        Set<DirectedGraphNode> set = new HashSet<>();
        
        for (DirectedGraphNode startNode : startNodes) {
            queue.offer(startNode);
        }
        
        while (!queue.isEmpty()) {
            DirectedGraphNode node = queue.poll();
            results.add(node);
            for (DirectedGraphNode neighbor : node.neighbors) {
                indegree.put(neighbor, indegree.get(neighbor) - 1);
                if (indegree.get(neighbor) == 0) {
                    queue.offer(neighbor);
                }
            }
        }
        
        return results;
    }
}
```
# Time complexity
O(V + E)

# Notes and Tips
1.  In java, we can not directly change the value of HashMap. To acheive this, We must reinsert the pair with the same key value.
2.  To traverse a Map, we can traverse its keySet. 
3.  For normal array like `String[]`, we can use `String[].length`, but for `ArrayList` we must use `size()`.