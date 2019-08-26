# Algorithm

Linked list reverse 

# Better solution

Currently Best

## Performance:

Runtime: 3 ms, faster than 97.63% of Java online submissions for Sort List.

Memory Usage: 39.3 MB, less than 100.00% of Java online submissions for Sort List.

## Time spent:

20 min 54 seconds 

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
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        } 
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        //Notation : Remember to add dummy, otherwise if the length of the link list is 2, slow will be equal to fast, which points to node2. 
        ListNode slow = dummy, fast = dummy;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        ListNode head2 = slow.next;
        slow.next = null;
        
        head = sortList(head);
        head2 = sortList(head2);
        return merge(head, head2);
    }
    
    private ListNode merge(ListNode head, ListNode head2) {
        ListNode dummy = new ListNode(0);
        ListNode cur1 = head;
        ListNode cur2 = head2;
        ListNode prev = dummy;
        
        while (cur1 != null && cur2 != null) {
            if (cur1.val <= cur2.val) {
                prev.next = cur1;
                cur1 = cur1.next;
                prev = prev.next;
            } else {
                prev.next = cur2;
                cur2 = cur2.next;
                prev = prev.next;
            }
        }
        
        if (cur1 != null) {
            prev.next = cur1;
        }
        
        if (cur2 != null) {
            prev.next = cur2;
        }
        
        return dummy.next;
    }
}
```



# Time complexity

O(n)

# Notes and Tips

1. Remember to add dummy, otherwise if the length of the link list is 2, slow will be equal to fast, which points to node2. 