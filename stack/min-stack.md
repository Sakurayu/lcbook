# Min Stack

[**155. Min Stack**](https://leetcode.com/problems/min-stack/description/)

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

* push\(x\) -- Push element x onto stack.
* pop\(\) -- Removes the element on top of the stack.
* top\(\) -- Get the top element.
* getMin\(\) -- Retrieve the minimum element in the stack.

**Example:**

```text
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

**My Solutions:**

min stack的push, top, pop和stack一样，多一个getMin\(\) 会返回stack中最小值，因此需要记住stack中的最小值

1。 方法1：用两个stack

```text
class MinStack {
    Stack<Integer> stack, minStack;
    
    public MinStack() {
        stack = new Stack<Integer>();
        minStack = new Stack<Integer>();
    }
    
    public void push(int x) {
        stack.push(x);
        if (!minStack.isEmpty()) {
            
             //"<=" for duplicate numbers
            if (x <= minStack.peek()) minStack.push(x); 
        } else {
            minStack.push(x);
        }
    }
    
    public void pop() {
        int x = stack.pop();
        if (!minStack.isEmpty()) {
            if (x == minStack.peek()) minStack.pop();
        }
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        if (!minStack.isEmpty()) return minStack.peek();
        else return stack.peek();
        
    }
}
```

2。 方法2：用一个stack

```text
class MinStack {

    Stack<Integer> stack;
    int min;
    
    public MinStack() {
        stack = new Stack<Integer>();
        min = Integer.MAX_VALUE;
    }
    
    //push two times, the up one is the min, 
    //the second is the second smallest
    public void push(int x) { 
         if (x <= min) {
            stack.push(min);
            min = x;
        }
        stack.push(x);
    }
    
     //if pop out the min, set the min to be the second smallest
    public void pop() {
        if (stack.peek() == min) { 
            stack.pop();
            min = stack.pop();
        } else {
            stack.pop();
        }
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return min;
    }
}
```

