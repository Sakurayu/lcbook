# 681. Next Closest Time

## 681. Next Closest Time

Given a time represented in the format “HH:MM”, form the next closest time by reusing the current digits. There is no limit on how many times a digit can be reused.

You may assume the given input string is always valid. For example, “01:34”, “12:09” are all valid. “1:34”, “12:9” are all invalid.

```text
Example 1:
Input: "19:34"
Output: "19:39"
Explanation: The next closest time choosing from digits 1, 9, 3, 4, is 19:39, which occurs 5 minutes later.  It is not 19:33, because this occurs 23 hours and 59 minutes later.1234
```

```text
Example 2:
Input: "23:59"
Output: "22:22"
Explanation: The next closest time choosing from digits 2, 3, 5, 9, is 22:22. It may be assumed that the returned time is next day's time since it is smaller than the input time numerically.1234
```

_**My Solutions：**_

 这道题给了一个时间点，求最近的下一个时间点，规定了不能产生新的数字，当下个时间点超过零点时，就当第二天的时间。

为了找到下一个时间点，从分钟开始换数字，而且换的数字要是存在的数字，那么先要做的就是统计当前时间点中的数字，由于可能有重复数字的存在，用一个伪哈希表来存给的时间的数字。

下面就从低位分钟开始换数字了，如果低位分钟上的数字已经是最大的数字了，那么说明要转过一轮了，就要把低位分钟上的数字换成最小的那个数字；否则就将低位分钟上的数字换成下一个数字。换一种说法就是，去哈希表里找有没有比给定的这个数大而且合法的数字，如果有则返回带有这个合法数字的新的string；如果没有，就把这一位设为哈希表里的最小值。然后再看高位分钟上的数字，同理，如果高位分钟上的数字已经是最大的数字，或则下一个数字大于5，那么直接换成最小值；否则就将高位分钟上的数字换成下一个数字。

对于小时位上的数字也是同理。当小时高位不为2的时候，低位可以是0~9，而当高位为2时，低位需要小于等于3。对于小时高位，其必须要小于等于2。

时间复杂度: O\(4\*10\)

空间复杂度: O\(10\)

```text
public String nextClosestTime(String time) {
        char[] t = time.toCharArray(), result = new char[4];
        int[] list = new int[10]; //数字集合
        char min = '9'; //记录最小的数
        
        for (char c : t) {
            if (c == ':') continue;
            list[c - '0']++;
            if (c < min) {
                min = c;
            }
        }
        
        //分钟最低位，如果有比最低位大的数字，直接返回
        for (int i = t[4] - '0' + 1; i <= 9; i++) {
            if (list[i] != 0) {
                t[4] = (char)(i + '0');
                return new String(t);
            }
        }
        //如果没有，则把第四位设为最小值
        t[4] = min;
        
        //分钟高位，如果有比最低位大的数字且此数字<=5，直接返回
        for (int i = t[3] - '0' + 1; i <= 5; i++) {
            if (list[i] != 0) {
                t[3] = (char)(i + '0');
                return new String(t);
            }
        }
        //如果没有，则把第三位设为最小值
        t[3] = min;
        
        //检查时钟第一位是0/1 还是2。如果是0/1,stop是9，因为最多到09或19；不然stop是3，最多到23
        int stop = t[0] < '2' ? 9 : 3;
        
        for (int i = t[1] - '0' + 1; i <= stop; i++) {
            if (list[i] != 0) {
                t[1] = (char)(i + '0');
                return new String(t);
            }
        }
        t[1] = min;
        
        for (int i = t[0] - '0' + 1; i <= 2; i++) {
            if (list[i] != 0) {
                t[0] = (char)(i + '0');
                return new String(t);
            }
        }
        t[0] = min;
        
        return new String(t);
}
```

 原题 -&gt; closest time after + 不可重复使用数字 -&gt; closest time before + （可重复使用数字 or 不可重复使用数字）

Follow Up 1:

如果是closest time after + 不可重复使用数字。

e.g，



19：34 ==&gt; 19:43，情况1

16：29 ==&gt; 19:26，情况2

23：26 ==&gt; 22:36 next day，情况2

15：58 ==&gt; 18:58 ，情况2

22：23 ==&gt; 23:22，情况2

12：49 ==&gt; 21:49，情况3

19：29 ==&gt; 19:29

23：55 ==&gt; 23:55

先看分钟，如果可以只靠移动分钟数改变最简单。需要满足的条件是十位数小于个位数且个位数&lt;=5。不然的话必然需要移动时钟数。--情况1

再看时钟。如果第一个是0/1，低位数最多是9；如果第一个是2，低位数最多是3。如果分钟数两数中，有比时钟低位数大的数，且分钟数小于等于9/3, 选择分钟数里较小的数放在低位。剩下两个数小一点的数必须小于等于5。--情况2

如果不满足以上条件，但是时钟高位是1，且后面的数字里有2的，以及剩余两个数字有一个小于等于5的，时钟变成21， 剩余数字按大小排列。 --情况3

剩余情况无法变化，是24小时候的本身。



Follow Up 2:

如果是closest time before + 可重复使用数字, 比如 12：34，答案是12：33。

下面就从低位分钟开始换数字了，如果低位分钟上的数字已经是最小的数字了，那么说明要回转过一轮了，就要把低位分钟上的数字换成最大的那个数字；否则就将低位分钟上的数字换成次小的数字。换一种说法就是，去哈希表里找有没有比给定的这个数小而且合法的数字，如果有则返回带有这个合法数字的新的string；如果没有，就把这一位设为哈希表里的最大值。然后再看高位分钟上的数字，同理，如果高位分钟上的数字已经是最小的数字，或则下一个数字大于5，那么直接换成最小值；否则就将高位分钟上的数字换成下一个数字。

对于小时位上的数字也是同理。当小时高位不为2的时候，低位可以是0~9，而当高位为2时，低位需要小于等于3。对于小时高位，其必须要小于等于2。

```text
public String nextClosestTime(String time) {
        char[] t = time.toCharArray(), result = new char[4];
        int[] list = new int[10]; //数字集合，0~9
        char max = '0'; //记录最大的数
        
        for (char c : t) {
            if (c == ':') continue;
            list[c - '0']++;
            if (c > max) {
                max = c;
            }
        }
        
        //分钟最低位，如果有比最低位小的数字，直接返回。eg，12：34变成12：33
        for (int i = t[4] - '0' - 1; i >= 0; i--) {
            if (list[i] != 0) {
                t[4] = (char)(i + '0');
                return new String(t);
            }
        }
        //如果没有，则把第四位设为最大值
        t[4] = max;
        
        //分钟高位，如果有比最低位小的数字且此数字<=5，直接返回。
        //eg, 22：21上一步变成22：22，这一步变成22：12
        for (int i = t[3] - '0' - 1; i >= 0 && i <= 5; i--) {
            if (list[i] != 0) {
                t[3] = (char)(i + '0');
                return new String(t);
            }
        }
        //如果没有，则把第三位设为最大值
        t[3] = max;
        
        //检查时钟第一位是0/1 还是2。如果是0/1,stop是9，因为时钟位最多到09或19；不然stop是3，最多到23
        int stop = t[0] < '2' ? 9 : 3;
        
         //时钟最低位，如果有比此位数小的数字，直接返回
         //eg, 21：11第一步变成21：12，第二步变成21：22，这一步变成22：22
        for (int i = t[1] - '0' - 1; i >= 0 && i <= stop; i--) {
            if (list[i] != 0) {
                t[1] = (char)(i + '0');
                return new String(t);
            }
        }
        t[1] = max;
        
        //时钟高位，如果有比此位数小的数字，直接返回
         //eg, 21：11第一步变成21：12，第二步变成21：22，第三步变成22：22，这一步变成12：22
        for (int i = t[0] - '0' + 1; i >= 0 && i <= 2; i--) {
            if (list[i] != 0) {
                t[0] = (char)(i + '0');
                return new String(t);
            }
        }
        t[0] = max;
        
        return new String(t);
}
```

