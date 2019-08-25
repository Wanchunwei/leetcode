# Algorithm

Linked list reverse 

# Better solution

Currently Best

## Performance:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Nodes in k-Group.

Memory Usage: 38.8 MB, less than 24.14% of Java online submissions for Reverse Nodes in k-Group.

## Time spent:

41 min 09 seconds 

## Times of Wrong answer:

None

## Solution

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || k < 2) {
            return head;
        }
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;
        while (prev != null) {
            prev = reverseKGroupNodes(prev, k);
        }
        
        return dummy.next;
    }
    
    private ListNode reverseKGroupNodes(ListNode prev, int k) {
        ListNode cur = prev.next;
        for (int i = 0; i < k; i++) {
            if (cur == null) {
                return null;
            }
            cur = cur.next;
        }
        
        ListNode nodeKplus = cur;
        ListNode node1 = prev.next;
        ListNode pre = prev;
        ListNode head = prev.next;
        while (head != nodeKplus) {
            ListNode nextNode = head.next;
            head.next = pre;
            pre = head;
            head = nextNode;
        }
        
        node1.next = nodeKplus;
        prev.next = pre;
        return node1;
    }
}
```



# Time complexity

O(n)

# Notes and Tips

