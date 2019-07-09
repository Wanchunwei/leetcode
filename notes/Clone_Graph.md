# Algorism 

BFS

Analysis:
1. Find all nodes. 
2. Create a HashMap to store mapping relationship of original and new Nodes in order to find corresponding nodes when adding edges. 
3. Add edges to new Graph.

# Better solution 

DFS(Recursion)

# Solution 

## Performans:

Runtime: 2 ms, faster than 53.66% of Java online submissions for Clone Graph.

Memory Usage: 33.6 MB, less than 98.68% of Java online submissions for Clone Graph.

## Time spent:

Not Done

## Times of Wrong answer:

1 - Bug 1

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;

    public Node() {}

    public Node(int _val,List<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/
class Solution {
    public Node cloneGraph(Node node) {
        if (node == null) {
            return node;
        }
        
        List<Node> nodes = getAllNodes(node);
        
        Map<Node, Node> mapping = new HashMap<>();
        for (Node n : nodes) {
            mapping.put(n, new Node(n.val, new ArrayList<Node>()));
        }
        
        for (Node n : nodes) {
            Node newNode = mapping.get(n);
            for (Node neighbors : n.neighbors) {
                Node newNeighbor = mapping.get(neighbors);
                newNode.neighbors.add(newNeighbor);
            }
        }
        
        return mapping.get(node);
    }
    
    private List<Node> getAllNodes(Node node) {
        Queue<Node> queue = new LinkedList<>();
        List<Node> nodes = new ArrayList<>();
        
        queue.offer(node);
        nodes.add(node);
        while (!queue.isEmpty()) {
            Node temp = queue.poll();
            for (Node n : temp.neighbors) {
                //Bug 1: When doing BFS in a graph, be careful about not to form a loop. 
                if (!nodes.contains(n)) {
                    queue.offer(n);
                    nodes.add(n);
                }
            }
        }
        
        return nodes;
    }
}
```

# Time complexity
O(n)

# Notes and Tips
1. When doing BFS in a graph, be careful about not to form a loop. Do 
```java
if (!nodes.contains(n)) {
    queue.offer(n);
    nodes.add(n);
}
```
2. Take step by step analysis clearly when coding. 
3. Create a HashMap to mapping original and new nodes. 