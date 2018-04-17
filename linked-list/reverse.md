# Reverse

[**206. Reverse Linked List**](https://leetcode.com/problems/reverse-linked-list/description/)

 **My Solutions:**

Time: O\(n\); Space: O\(1\)

```text
public ListNode reverseList(ListNode head) {
    if (head == null || head.next == null) return head;
    ListNode pre = null;
    while (head != null) {
        ListNode temp = head.next;
        head.next = pre;
        pre = head;
        head = temp;
    }
    return pre;
}
```

* recursive version

```text
public ListNode reverseList(ListNode head) {
    if (head == null || head.next == null) return head;
    ListNode newHead = reverseList(head.next);
    head.next.next = head;
    head.next = null;
    return newHead;
}
```

[**92. Reverse Linked ListII**](https://leetcode.com/problems/reverse-linked-list-ii/description/)

Reverse a linked list from position _m_ to _n_. Do it in-place and in one-pass.

For example:  
Given `1->2->3->4->5->NULL`, _m_ = 2 and _n_ = 4,

return `1->4->3->2->5->NULL`.

**Note:**  
Given _m_, _n_ satisfy the following condition:  
1 ≤ _m_ ≤ _n_ ≤ length of list.

 **My Solutions:**

只反转从m到n位置的nodes，所以需要先走到m之前的位置，然后反转到n-m的位置

Time: O\(n\); Space: O\(1\)

```text
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (head == null || m > n) return null;

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy;
        for (int i = 0; i < m - 1; i++) pre = pre.next; //find the node right before the reversed one

        ListNode first = pre.next;
        ListNode second = first.next;

        for (int i = 0; i < n - m; i++) {
            first.next = second.next;
            second.next = pre.next;
            pre.next = second;
            second = first.next;
        }

        return dummy.next;
    }
}
```

