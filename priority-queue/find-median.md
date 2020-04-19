# 295. Find Median from Data Stream

 [**295. Find Median from Data Stream**](https://leetcode.com/problems/find-median-from-data-stream/description/)\*\*\*\*

_**My Solutions:**_

维持两个priority queue。假设有5个数字，minQ 储存最小的两个，maxQ储存较大的三个，median在maxQ的最上。如果是双数个数字，median是两个pq最上的平均值。

因为pq会自动维护从小到大排列， pq.peek\(\) or pq.poll\(\)返回最上面的最小数字。所以在minQ中储存的其实是负数。比如minQ要储存【-2，-1】。

因此，在add元素时，先把数字加入maxQ，再把maxQ上的最小数字变成负数，加入minQ，如果maxQ数字数量小于minQ了，再把minQ上的最小数字（此时为负数）变成正数，重新加入maxQ。

e.g.

add\(1\), maxQ = \[1\], minQ = \[\]

add\(2\), maxQ = \[2\], minQ = \[-1\]

add\(3\), maxQ = \[2,3\], minQ = \[-1\]

add\(4\), maxQ = \[3, 4\], minQ = \[-2, -1\] 

```text
class MedianFinder {

    private Queue<Integer> minQ = new PriorityQueue<>();
    private Queue<Integer> maxQ = new PriorityQueue<>();
    /** initialize your data structure here. */
    public MedianFinder() {
        
    }
    
    public void addNum(int num) {
        maxQ.add(num);
        minQ.add(-maxQ.poll());
        if (maxQ.size() < minQ.size()) maxQ.add(-minQ.poll());
    }
    
    public double findMedian() {
        return maxQ.size() > minQ.size() ? maxQ.peek() : (maxQ.peek() - minQ.peek()) / 2.0;
    }
}
```



