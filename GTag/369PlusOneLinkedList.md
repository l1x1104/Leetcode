[链表加一运算](https://leetcode.com/problems/plus-one-linked-list/description/)

```java
class Solution {
    public ListNode plusOne(ListNode head) {
        ListNode curr = head; 
        ListNode newHead = reverseList(curr);
        curr = newHead;
    
        while(curr != null) {
            if(curr.val != 9) {
                curr.val = 1 + curr.val;
                break;
            }
            else {
                if(curr.next == null && curr.val == 9) {
                    curr.val = 0;
                    curr.next = new ListNode(1);
                    break;
                }
                curr.val = 0;
                curr = curr.next;
            }
        }
        return reverseList(newHead);
        
    }
    private ListNode reverseList(ListNode head) {
        ListNode prev = null;
        while(head != null) {
            ListNode next = head.next;
            head.next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }
}
```
