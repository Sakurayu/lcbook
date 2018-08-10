# Copy

\*\*\*\*[ **138. Copy List with Random Pointer**](https://leetcode.com/problems/copy-list-with-random-pointer/description/)\*\*\*\*

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

_**My Solutions:**_

方法1：用hashmap储存node和node‘，Time: O\(n\); Space: O\(n\)

```text
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if(head == null) return null;
        
        RandomListNode dummy = new RandomListNode(0);
        RandomListNode curr = dummy;
        
        //use hashmap to avoid copying multiple times for same node, it stores node and node'
        //e.g. map.put(1, 1');
        Map<RandomListNode, RandomListNode> map = new HashMap<>();
        
        while (head != null) {
            
            //put node' into the list
            if (!map.containsKey(head)) map.put(head, new RandomListNode(head.label));
            curr.next = map.get(head);
            
            //link node' with it's random
            if (head.random != null) {
                if (!map.containsKey(head.random)) map.put(head.random, new RandomListNode(head.random.label));
                curr.next.random = map.get(head.random);
            }
            
            head = head.next;
            curr = curr.next;
        }
        
        return dummy.next;
    }
}
```

方法2：in place， Time: O\(n\); Space: O\(1\)

```text
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if(head == null) return null;
        
        //for each node, insert a copied node between node and node.next
        //e.g. 1-->1'-->2-->2'-->3-->3'...
        RandomListNode curr = head;
        while (curr != null) {
            RandomListNode copy = new RandomListNode(curr.label);
            copy.next = curr.next;
            curr.next = copy;
            curr = curr.next.next;
            
        }
        
        //for each copied node, it's random is the original node's random's next, which is also a copied node
        //each copied node is curr.next
        //e.g. 1.random = 3, then 1.next.random = 3.next (1' --> 3')
        curr = head;
        while (curr != null) {
            if (curr.random != null) curr.next.random = curr.random.next;
            curr = curr.next.next;
        }
        
        //extract copied nodes
        curr = head;
        RandomListNode dummy = new RandomListNode(0);
        RandomListNode copyHead = dummy;
        while (curr != null) {
            copyHead.next = curr.next; //curr.next is the copied node
            curr.next = curr.next.next; //curr.next becomes the next original node
            copyHead = copyHead.next; //copyHead moves forward
            curr = curr.next; //curr moves forward
            
        }
        return dummy.next;
    }
}
```

