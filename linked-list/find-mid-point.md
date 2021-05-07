# Find Mid-Point

* 无论单数（1，2，3）或双数（1，2，3，4），slow停在2 

```text
public ListNode findMiddle(ListNode head) {
    if (head == null || head.next == null) return head;
    ListNode slow = head, fast = head.next;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next;
    }
    return slow;
}
```

或者

* slow和fast同时起跳，slow一次跳一步，fast一次跳两步。当fast跳到最后一个数字的时候，slow在中点
* fast.next != null && fast.next.next != null 是为了确保至少有3个数。因为如果只有两个数，直接返回第一个

```text
public ListNode findMiddle(ListNode head) {
    if (head == null || head.next == null) return head;
    ListNode slow = head, fast = head;
    while (fast.next != null && fast.next.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
}
```

