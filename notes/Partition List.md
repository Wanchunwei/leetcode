# Algorithm

Linked list reverse 

# Better solution

Currently Best

## Performance:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Partition List.

Memory Usage: 36 MB, less than 100.00% of Java online submissions for Partition List.

## Time spent:

10 min 

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
    public ListNode partition(ListNode head, int x) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode dummy1 = new ListNode(0);
        ListNode prev1 = dummy1;
        ListNode dummy2 = new ListNode(0);
        ListNode prev2 = dummy2;
        ListNode start = head;
        
        while (start != null) {
            if (start.val < x) {
                prev1.next = start;
                prev1 = prev1.next;
                start = start.next;
            } else {
                prev2.next = start;
                prev2 = prev2.next;
                start = start.next;
            }
        }
        //Notation : Remember to set the prev.next = null, otherwise cycle list may exist.
        prev1.next = null;
        prev2.next = null;
        
        prev1.next = dummy2.next;
        return dummy1.next;
    }
}
```



# Time complexity

O(n)

# Notes and Tips

1. Remember to set the prev.next = null, otherwise cycle list may exist.