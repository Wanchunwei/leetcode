# Algorithm

Linked list reverse 

# Better solution

Currently Best

## Performance:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Linked List II.

Memory Usage: 34.2 MB, less than 100.00% of Java online submissions for Reverse Linked List II.

## Time spent:

8 min 58 seconds 

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
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (head == null || head.next == null || m == n) {
            return head;
        }
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode prev = dummy;
        ListNode cur = head;
        int count = m;
        while (count > 1) {
            prev = prev.next;
            cur = cur.next;
            count--;
        }
        
        prev.next = reverseList(cur, n - m + 1);
        return dummy.next;
    }
    
    private ListNode reverseList(ListNode head, int length) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode node1 = head;
        ListNode prev = dummy;
        while (length > 0) {
            ListNode nextNode = head.next;
            head.next = prev;
            prev = head;
            head = nextNode;
            length--;
        }
        
        dummy.next = prev;
        node1.next = head;
        return dummy.next;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

