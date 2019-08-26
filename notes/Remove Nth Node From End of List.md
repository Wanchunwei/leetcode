# Algorithm

Linked list reverse 

# Better solution

Currently Best

## Performance:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Remove Nth Node From End of List.

Memory Usage: 34.8 MB, less than 100.00% of Java online submissions for Remove Nth Node From End of List.

## Time spent:

5 min 53 seconds 

## Times of Wrong answer:

1 - Bug 1

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) {
            return head;
        }
        
        ListNode cur = head;
        int length = 0;
        while (cur != null) {
            length++;
            cur = cur.next;
        }
        
        int move = length - n;
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;
        ListNode current = head;
        while (move > 0) {
            current = current.next;
            prev = prev.next;
            move--;
        }
        
        prev.next = current.next;
        //Bug 1 : Don't return head, otherwise corner case that if we remove the head, it will fail.
        return dummy.next;
    }
}
```



# Time complexity

O(n)

# Notes and Tips

1. Don't return head, otherwise corner case that if we remove the head, it will fail;