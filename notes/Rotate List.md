# Algorithm

Linked list reverse 

# Better solution

Currently Best

## Performance:

Runtime: 0 ms, faster than 100.00% of Java online submissions for Rotate List.

Memory Usage: 38.6 MB, less than 56.90% of Java online submissions for Rotate List.

## Time spent:

9 min 15 seconds 

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
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode prev = head;
        int length = 1;
        while (prev.next != null) {
            length++;
            prev = prev.next;
        }

        prev.next = head;
        int move = length - k % length;
        while (move > 0) {
            prev = prev.next;
            head = head.next;
            move--;
        }

        prev.next = null;
        return head;
    }
}
```



# Time complexity

O(n)

# Notes and Tips

