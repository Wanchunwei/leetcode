# Algorithm

Two Pointers

# Better Solution

Currently Best

## Performance:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Linked List Cycle.

Memory Usage: 37.1 MB, less than 100.00% of Java online submissions for Linked List Cycle.

## Time spent:

5 min 

## Times of Wrong answer:

None

## Solution

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head, slow = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) {
                return findMeetPoint(head, fast);
            }
        }
        return null;
    }
    
    private ListNode findMeetPoint(ListNode head, ListNode fast) {
        ListNode cur = head;
        while (cur != fast) {
            cur = cur.next;
            fast = fast.next;
        }
        return cur;
    }
}
```

# Time complexity

O(n)

# Notes and Tips

