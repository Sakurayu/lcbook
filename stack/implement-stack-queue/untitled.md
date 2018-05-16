# 225. Implement Stack using Queues

[ **225. Implement Stack using Queues**](https://leetcode.com/problems/implement-stack-using-queues/description/)

Implement the following operations of a stack using queues.

* push\(x\) -- Push element x onto stack.
* pop\(\) -- Removes the element on top of the stack.
* top\(\) -- Get the top element.
* empty\(\) -- Return whether the stack is empty.

**Notes:**

* You must use only standard operations of a queue -- which means only `push to back`, `peek/pop from front`, `size`, and `is empty` operations are valid.
* Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque \(double-ended queue\), as long as you use only standard operations of a queue.
* You may assume that all operations are valid \(for example, no pop or top operations will be called on an empty stack\).

**My Solutions:**

example:  

* 原有元素1，2； 加入3. queue是linkedlist
* 用两个queue实现的时候，需要用一个top记录最上面的，保证top\(\) 时间复杂度为1

1。 方法1：Two Queues, push: O\(1\), pop: O\(n\)

* push: q1.add\(3\)
* pop：
  * q2.add\(q1.remove\(\)\) （除了最后加入的那个元素，因为需要pop出）--&gt; q2 此时为（1，2）。
  * temp = q1; q1 = q2; q2 = temp. 
  * q1\(1, 2\), q2为空

```text
class MyStack {
    
    Queue<Integer> q1 = new LinkedList<>();
    Queue<Integer> q2 = new LinkedList<>();
    int top;

    /** Initialize your data structure here. */
    public MyStack() {
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        q1.add(x);
        top = x;
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        while(q1.size() > 1) {
            top = q1.remove();
            q2.add(top);
        }
        Queue<Integer> temp = q1;
        q1 = q2;
        q2 = temp;
        return q2.remove();
    }
    
    /** Get the top element. */
    public int top() {
        return top;
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
       return q1.isEmpty();
    }
}
```

2。 方法2： Two Queues, push: O\(n\), pop: O\(1\)

* push：
  * q2.add\(3\)
  * 当q1 不为空时，e.g., q1\(2,1\), 把q2.add\(q1.remove\(\)\) --&gt; q2\(3,2,1\),q1为空
  * temp = q1; q1 = q2; q2 = temp
  * q1\(3,2,1\), q2 为空
* pop：
  * q1.remove

3。 方法3： One Queues, push: O\(n\), pop: O\(1\)

* push:
  * q1.add\(3\) //此时q1\(3, 2,1\)
  * 算出size = q1.size\(\)。 只要size &gt; 1，q1.add\(q1.remove\(\)\); size--;
  * q1\(3, 2, 1\) --&gt; \(2, 1, 3\) --&gt; \(1, 3, 2\) --&gt; \(3, 2, 1\)
* pop: q1.remove







