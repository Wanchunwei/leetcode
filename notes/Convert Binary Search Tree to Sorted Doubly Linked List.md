# Algorithm 

Divide conquer

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 23.76% of Java online submissions for Convert Binary Search Tree to Sorted Doubly Linked List.

Memory Usage: 36.1 MB, less than 6.14% of Java online submissions for Convert Binary Search Tree to Sorted Doubly Linked List.

## Time spent:

14 min 24 seconds

## Times of Wrong answer:

None

# Solution 

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;

    public Node() {}

    public Node(int _val,Node _left,Node _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {
    public Node treeToDoublyList(Node root) {
        Queue<Node> queue = new LinkedList<>();
        helper(root, queue);
        return constructLinkList(queue);
    }
    
    private void helper(Node root, Queue<Node> queue) {
        if (root != null) {
            if (root.left != null) {
                helper(root.left, queue);
            }
            queue.offer(root);
            if (root.right != null) {
                helper(root.right, queue);
            }
        }
    }
    
    private Node constructLinkList(Queue<Node> queue) {
        if (queue.isEmpty()) {
            return null; 
        } else {
            Node preSuccessor = queue.poll();
            Node start = preSuccessor;
            while (!queue.isEmpty()) {
                Node successor = queue.poll();
                preSuccessor.right = successor;
                successor.left = preSuccessor;
                preSuccessor = successor;
            }
            
            preSuccessor.right = start;
            start.left = preSuccessor;
            
            return start;
        } 
    }
}
```

# Time complexity

O(n)

# Note and tips

