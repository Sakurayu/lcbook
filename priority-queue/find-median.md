# 295. Find Median from Data Stream

 [**295. Find Median from Data Stream**](https://leetcode.com/problems/find-median-from-data-stream/description/)\*\*\*\*

_**My Solutions:**_

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



