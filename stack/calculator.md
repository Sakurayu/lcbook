# Calculator

 [**224. Basic Calculator**](https://leetcode.com/problems/basic-calculator/description/)

 The expression string may contain open `(` and closing parentheses `)`, the plus `+` or minus sign `-`, **non-negative** integers and empty spaces .

You may assume that the given expression is always valid.

Some examples:

```text
"1 + 1" = 2
" 2-1 + 2 " = 3
"(1+(4+5+2)-3)+(6+8)" = 23
```

**My Solutions:**

stack 储存的是括号前的符号。括号内的每一个数字加入result时，都要peek一下stack里的符号，相乘之后，再加入result。e.g. -\(3 - 6\) ， result -3+6

```text
class Solution {
    public int calculate(String s) {
        s = s.replace(" ", ""); //去掉空格
        int len = s.length(), sign = 1, res = 0, i = 0;
        Stack<Integer> stack = new Stack<>();
        stack.push(1); //一开始设置为正号
        while (i < len) {
            char c = s.charAt(i);
            
            if (c == '+') {
                sign = 1;
                i++;
            } else if (c == '-') {
                sign = -1; 
                i++;
            } else if (c == '(') {
                stack.push(sign * stack.peek()); //stack里有（1, -1）
                sign = 1;
                i++;
            } else if (c == ')') {
                stack.pop();
                i++;
            } else {
                int num = 0;
                //判断是否超出边界或者不是digit(不再是一个数字)
                while (i < len && Character.isDigit(s.charAt(i))) {
                    num = num * 10 + s.charAt(i) - '0';
                    i++;
                }
                res += num * sign * stack.peek();
            }
        }
        return res;
        
    }
}
```

#### [227. Basic Calculator II](https://leetcode.com/problems/basic-calculator-ii/description/)

The expression string contains only **non-negative** integers, `+`, `-`, `*`, `/` operators and empty spaces . The integer division should truncate toward zero.

You may assume that the given expression is always valid.

Some examples:

```text
"3+2*2" = 7
" 3/2 " = 1
" 3+5 / 2 " = 5
```

**My Solutions:**

stack储存+-\*/前的数字。最终，stack储存了所有可以相加的项，再把

stack里的元素相加起来

e.g., 3 \* 2 - 5

* 碰到3： stack：空； sign = +； num = 3
* 碰到\*： stack： 3； sign = \*； num = 0
* 碰到2： num = 2； 
* 碰到-： \(stack pop出3，再push进6\)stack: 6；sign = -; num = 0
* 碰到5：num = 5；
  * 进入下一个if block，因为5是最后一个数字
  * stack：6， -5



```text
class Solution {
    public int calculate(String s) {
        if (s == null || s.length() == 0) return 0;
        Stack<Integer> stack = new Stack<>();
        int num = 0; //num放在外面
        char sign = '+'; //sign 储存的是数字之前的符号
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (Character.isDigit(c))
                num = num * 10 + c - '0';
            
            if ((!Character.isDigit(c) && c != ' ') || i == s.length() - 1) {
                if (sign == '+') stack.push(num); //stack只储存最后可以相加的项
                else if (sign == '-') stack.push(-num);  //把数字变为负号，stack只储存最后可以相加的项
                else if (sign == '*') stack.push(stack.pop() * num);  //把之前的数字pop出来，做乘运算，stack 只储存最后可以相加的项
                else if (sign == '/') stack.push(stack.pop() / num);   //把之前的数字pop出来，做除运算，stack 只储存最后可以相加的项
                sign = c; //符号更新成现在的char
                num = 0;
            }
        }
        
        //相加所有数字
        int res = 0; 
        for (int i: stack) res += i;
        return res;
    }
}
```

[  
](https://leetcode.com/problems/basic-calculator-ii/description/)

