# Algorithm

Linked list reverse 

# Better solution

Currently Best

## Performance:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Copy List with Random Pointer.

Memory Usage: 33.6 MB, less than 99.07% of Java online submissions for Copy List with Random Pointer.

## Time spent:

24 min 03 seconds 

## Times of Wrong answer:

1- Bug 1

## Solution

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node next;
    public Node random;

    public Node() {}

    public Node(int _val,Node _next,Node _random) {
        val = _val;
        next = _next;
        random = _random;
    }
};
*/
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return head;
        }
        
        head = copyListNode(head);
        head = copyRandomePointer(head);
        Node copyHead = splitCopyList(head);
        return copyHead; 
    }
    
    private Node copyListNode (Node head) {
        Node cur = head;
        while (cur != null) {
            Node nextNode = cur.next;
            Node newNode = new Node();
            newNode.val = cur.val;
            newNode.next = nextNode;
            cur.next = newNode;
            cur = nextNode;
        }
        return head;
    }
    
    private Node copyRandomePointer(Node head) {
        Node cur = head;
        Node curNew = head.next;
        while (cur != null) {
            if (cur.random == null) {
                curNew.random = null;
            } else {
                curNew.random = cur.random.next;
            }
            cur = curNew.next;
            //Bug 1 : Be careful of a corner case that the cur == null, then we can not do curNew = cur.next; 
            if (cur == null) {
                curNew = null;
            } else {
                curNew = cur.next;
            }
        }
        return head;
    }
    
    private Node splitCopyList(Node head) {
        Node dummy = new Node();
        dummy.val = 0;
        
        Node prev = dummy;
        Node cur = head;
        Node curNew = head.next;
        while (cur != null) {
            prev.next = curNew;
            cur.next = curNew.next;
            prev = curNew;
            cur = cur.next;
            if (cur == null) {
                curNew = null;
            } else {
                curNew = curNew.next.next; 
            }
        }
        
        return dummy.next;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

1. Be careful of a corner case that the `cur == null`, then we can not do `curNew = cur.next`; 