# 57. Insert Interval

 [**57. Insert Interval**](https://leetcode.com/problems/insert-interval/description/)\*\*\*\*

Given a set of _non-overlapping_ intervals, insert a new interval into the intervals \(merge if necessary\).

You may assume that the intervals were initially sorted according to their start times.

**Example 1:**

```text
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```

**Example 2:**

```text
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

My Solutions:

和56题思想差不多

```text
class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        if (intervals == null || newInterval == null) return intervals;
        
        List<Interval> list = new ArrayList<>();
        
        for (Interval i : intervals) {
            if (newInterval == null || i.end < newInterval.start) {
                list.add(i);
            } else if (i.start > newInterval.end) {
                list.add(newInterval);
                list.add(i);
                newInterval = null;
            } else {
                newInterval.start = Math.min(newInterval.start, i.start);
                newInterval.end = Math.max(newInterval.end, i.end);
            }
        }
        if (newInterval != null) list.add(newInterval);
        return list;
    }
}
```

