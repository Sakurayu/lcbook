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

1。 方法1：用两个stack。一个栈来按顺序存储 push 进来的数据，另一个栈去存最小值，也就是用栈顶保存当前所有元素的最小值。

push：stack 直接push，这个元素和minStack里peek的值比较：

* 如果新加入的元素大于栈顶元素，不操作
* 如果新加入的元素小于等于栈顶元素，pop进minStack

pop：记录下stack直接pop的值，然后：

* 如果这个值不是minStack里的最小值，不操作。
* 如果这个值也是minStack里的最小值，minStack也pop。

top：stack 直接peek。

getMin：

* 如果minStack不为空，从minStack peek
* 如果minStack为空，从stack peek

```text
入栈 3 
|   |    |   |
|   |    |   |
|_3_|    |_3_|
stack  minStack

入栈 5 ， 5 大于 minStack 栈顶，不处理
|   |    |   |
| 5 |    |   |
|_3_|    |_3_|
stack  minStack

入栈 2 ，此时右边的 minStack 栈顶就保存了当前最小值 2 
| 2 |    |   |
| 5 |    | 2 |
|_3_|    |_3_|
stack  minStack

出栈 2，此时右边的 minStack 栈顶就保存了当前最小值 3
|   |    |   |
| 5 |    |   |
|_3_|    |_3_|
stack  minStack

出栈 5，右边 minStack 不处理
|   |    |   |
|   |    |   |
|_3_|    |_3_|
stack  minStack

出栈 3
|   |    |   |
|   |    |   |
|_ _|    |_ _|
stack  minStack

作者：windliang
链接：https://leetcode-cn.com/problems/min-stack/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-38/
```

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

2。 方法2：用一个stack，和一个int min存最小值。

push：先比较当前值和min，如果当前值比min小，先把min push进去，更新min为当前值。最后再push当前值。这样保证stack的最顶端一定是最小值

pop：pop出来的值等于min，则需要再pop一次，把这个min的值更新。

top：stack直接peek

getMin：直接返回min

```text
入栈 3，3比MAX_INTEGER大，min=3
|   |    
|   |    
| 3 | 
|MAX|   
stack  

入栈 5，5 大于 min，min=3
|   |    
| 5 |    
| 3 |
|MAX|       
stack  

入栈 2 ，2比min小，先把min=3 push进去，再push2，min=2
| 2 | 
| 3 |    
| 5 |    
| 3 |
|MAX|       
stack 

出栈 2，pop出来的值2等于min，则需要再pop一次出来3，min=3  
| 5 |    
| 3 |
|MAX|       
stack 

出栈 5
|   |    
| 3 |
|MAX|       
stack 

出栈 3
|   |    
|   |    
|MAX|    
stack  
```

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
        if (min == stack.pop()) min = stack.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return min;
    }
}
```

