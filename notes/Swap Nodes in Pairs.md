# Algorithm

Linked list reverse 

# Better solution

Currently Best

## Performance:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Swap Nodes in Pairs.

Memory Usage: 34.3 MB, less than 100.00% of Java online submissions for Swap Nodes in Pairs.

## Time spent:

16 min 40 seconds 

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
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;
        while (prev != null) {
            prev = reverseAdjacent(prev, 2);
        }
        
        return dummy.next;
    }
    
    // 0->1->2->3 ==== 0->2->1->3
    private ListNode reverseAdjacent(ListNode prev, int count) {
        ListNode cur = prev.next;
        ListNode node1 = prev.next;
        int num = count;
        while (cur != null && num > 0) {
            num--;
            cur = cur.next;
        }
        
        if (num > 0) {
            return null;
        }
        
        ListNode node3 = cur;
        ListNode pre = prev;
        ListNode head = prev.next;
        while (head != node3) {
            ListNode temp = head.next;
            head.next = pre;
            pre = head;
            head = temp;
        }
        //0<-1<-2->3 == 0->2->1->3
        prev.next = pre;
        node1.next = node3;
        return node1;
    }
}
```



# Time complexity

O(n)

# Notes and Tips

