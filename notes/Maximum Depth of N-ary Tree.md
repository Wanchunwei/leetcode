# Algorithm 

Divide Conquer

# Better solution

Currently Best

## Performance:

Runtime: 1 ms, faster than 98.27% of Java online submissions for Maximum Depth of N-ary Tree.

Memory Usage: 46.5 MB, less than 52.29% of Java online submissions for Maximum Depth of N-ary Tree.

## Time spent:

7 min 33 seconds

## Times of Wrong answer:

1 - Bug 1

# Solution 

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val,List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
    public int maxDepth(Node root) {
        return helper(root);
    }
    
    private int helper(Node root) {
        //Bug 1 : Make clear what the variable stand for before initiate
        int depth = 0;
        if (root == null) {
            return depth;
        }
        
        //Notation : Don't invoke hepler() more than 1 time, otherwise it will time exceed.
        for (Node node : root.children) {
            int d = helper(node);
            depth = depth < d ? d : depth; 
        }
        
        return depth + 1;
    }
}
```

# Time complexity

O(n)

# Note and tips

1. Make clear what the variable stand for before initiate
2. Don't invoke hepler() more than 1 time, otherwise it will time exceed.