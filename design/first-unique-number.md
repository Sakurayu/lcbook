# First Unique Number

**First Unique Number**

You have a queue of integers, you need to retrieve the first unique integer in the queue.

Implement the `FirstUnique` class:

* `FirstUnique(int[] nums)` Initializes the object with the numbers in the queue.
* `int showFirstUnique()` returns the value of **the first unique** integer of the queue, and returns **-1** if there is no such integer.
* `void add(int value)` insert value to the queue.

**Example 1:**

```text
Input: 
["FirstUnique","showFirstUnique","add","showFirstUnique","add","showFirstUnique","add","showFirstUnique"]
[[[2,3,5]],[],[5],[],[2],[],[3],[]]
Output: 
[null,2,null,2,null,3,null,-1]

Explanation: 
FirstUnique firstUnique = new FirstUnique([2,3,5]);
firstUnique.showFirstUnique(); // return 2
firstUnique.add(5);            // the queue is now [2,3,5,5]
firstUnique.showFirstUnique(); // return 2
firstUnique.add(2);            // the queue is now [2,3,5,5,2]
firstUnique.showFirstUnique(); // return 3
firstUnique.add(3);            // the queue is now [2,3,5,5,2,3]
firstUnique.showFirstUnique(); // return -1

```

**Example 2:**

```text
Input: 
["FirstUnique","showFirstUnique","add","add","add","add","add","showFirstUnique"]
[[[7,7,7,7,7,7]],[],[7],[3],[3],[7],[17],[]]
Output: 
[null,-1,null,null,null,null,null,17]

Explanation: 
FirstUnique firstUnique = new FirstUnique([7,7,7,7,7,7]);
firstUnique.showFirstUnique(); // return -1
firstUnique.add(7);            // the queue is now [7,7,7,7,7,7,7]
firstUnique.add(3);            // the queue is now [7,7,7,7,7,7,7,3]
firstUnique.add(3);            // the queue is now [7,7,7,7,7,7,7,3,3]
firstUnique.add(7);            // the queue is now [7,7,7,7,7,7,7,3,3,7]
firstUnique.add(17);           // the queue is now [7,7,7,7,7,7,7,3,3,7,17]
firstUnique.showFirstUnique(); // return 17

```

**Example 3:**

```text
Input: 
["FirstUnique","showFirstUnique","add","showFirstUnique"]
[[[809]],[],[809],[]]
Output: 
[null,809,null,-1]

Explanation: 
FirstUnique firstUnique = new FirstUnique([809]);
firstUnique.showFirstUnique(); // return 809
firstUnique.add(809);          // the queue is now [809,809]
firstUnique.showFirstUnique(); // return -1

```

**Constraints:**

* `1 <= nums.length <= 10^5`
* `1 <= nums[i] <= 10^8`
* `1 <= value <= 10^8`
* At most `50000` calls will be made to `showFirstUnique` and `add`.

Hint \#1  Use doubly Linked list with hashmap of pointers to linked list nodes. add unique number to the linked list. When add is called check if the added number is unique then it have to be added to the linked list and if it is repeated remove it from the linked list if exists. When showFirstUnique is called retrieve the head of the linked list.   

Hint \#2  Use queue and check that first element of the queue is always unique.   

Hint \#3  Use set or heap to make running time of each function O\(logn\).

_**My Solutions:**_

方法1：用hashmap储存出现的value和次数，用queue储存出现的次序。但这个方法会超时

```text
class FirstUnique {
    
    Queue<Integer> q;
    HashMap<Integer, Integer> map;

    public FirstUnique(int[] nums) {
        q = new LinkedList<>();
        map = new HashMap<>();
        for (int n : nums) {
            this.add(n);
        }
    }
    
    public int showFirstUnique() {
        if (q.isEmpty()) return -1;
        while (!q.isEmpty()) {
            if (map.get(q.peek()) > 1) q.remove(); 
            else q.peek();
        }
        return -1;
    }
    
    public void add(int value) {
        if (map.containsKey(value)) map.put(value, map.get(value) + 1);
        else {
            q.add(value);
            map.put(value, 1);
        }
    }
}

/**
 * Your FirstUnique object will be instantiated and called as such:
 * FirstUnique obj = new FirstUnique(nums);
 * int param_1 = obj.showFirstUnique();
 * obj.add(value);
 */
```

方法2：用LinkedHashSet 储存只出现过一次的数字，用HashMap记录出现过的数字及其个数。

```text
class FirstUnique {
    
    LinkedHashSet<Integer> set; 
    HashMap<Integer, Integer> map;

    public FirstUnique(int[] nums) {
        set = new LinkedHashSet<>();
        map = new HashMap<>();
        for (int n : nums) {
            this.add(n);
        }
    }
    
    public int showFirstUnique() {
        return set.isEmpty() ? -1 : set.iterator().next();
    }
    
    public void add(int value) {
        map.put(value, map.getOrDefault(value, 0) + 1);
        if (map.get(value) == 1) set.add(value); 
        else set.remove(value);
    }
}
```



