# 729. My Calendar I

\*\*\*\*[ **729. My Calendar I**](https://leetcode.com/problems/my-calendar-i/submissions/1)\*\*\*\*

Implement a `MyCalendar` class to store your events. A new event can be added if adding the event will not cause a double booking.

Your class will have the method, `book(int start, int end)`. Formally, this represents a booking on the half open interval `[start, end)`, the range of real numbers `x` such that `start <= x < end`.

A double booking happens when two events have some non-empty intersection \(ie., there is some time that is common to both events.\)

For each call to the method `MyCalendar.book`, return `true` if the event can be added to the calendar successfully without causing a double booking. Otherwise, return `false` and do not add the event to the calendar.Your class will be called like this: `MyCalendar cal = new MyCalendar();` `MyCalendar.book(start, end)`

**Example 1:**

```text
MyCalendar();
MyCalendar.book(10, 20); // returns true
MyCalendar.book(15, 25); // returns false
MyCalendar.book(20, 30); // returns true
Explanation: 
The first event can be booked.  The second can't because time 15 is already booked by another event.
The third event can be booked, as the first event takes every time less than 20, but not including 20.
```

**Note:**

The number of calls to `MyCalendar.book` per test case will be at most `1000`.

In calls to `MyCalendar.book(start, end)`, `start` and `end` are integers in the range `[0, 10^9]`.

_**My Solutions：**_

方法1：对已有的每一个event检查与新event是否重叠

if \(old.start &lt;= start && old.end &gt; start\) return false; //已有event在新event之前开始，且在新event开始前并未结束（新event与旧event的后部重合,old.end可以==start，因为是\[ \) 区间）

if \(old.start &gt;= start && old.start &lt; end\) return false; //新event与旧event的前部重合

可以把以上两个条件合并，变成 old.start &lt; end && start &lt; old.end

时间：O\(n\)

```text
public class MyCalendar {
    List<int[]> calendar;

    MyCalendar() {
        calendar = new ArrayList();
    }

    public boolean book(int start, int end) {
        for (int[] iv: calendar) {
            if (iv[0] < end && start < iv[1]) return false;
        }
        calendar.add(new int[]{start, end});
        return true;
    }
}
```

方法2：利用treemap的性质优化

* floorKey\(target\)方法返回当前Map里小于target的key的最大值。
* ceilingKey\(target\)返回当前Map里大于target的key的最小值。

```text
class MyCalendar {
    
    TreeMap<Integer, Integer> calendar;

    public MyCalendar() {
        calendar = new TreeMap();
    }

    public boolean book(int start, int end) {
        Integer prev = calendar.floorKey(start), next = calendar.ceilingKey(start);
        if ((prev == null || calendar.get(prev) <= start) //prev is before start
            && (next == null || end <= next)) { //end is before next
            calendar.put(start, end);
            return true;
        }
        return false;
    }
}
```

时间：O\(lgn\)

