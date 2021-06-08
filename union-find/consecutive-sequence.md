# 128. Longest Consecutive Sequence

\*\*\*\*[**128. Longest Consecutive Sequence**](https://leetcode.com/problems/longest-consecutive-sequence/)\*\*\*\*

Given an unsorted array of integers `nums`, return _the length of the longest consecutive elements sequence._

You must write an algorithm that runs in `O(n)` time.

**Example 1:**

```text
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

**Example 2:**

```text
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

**Constraints:**

* `0 <= nums.length <= 105`
* `-109 <= nums[i] <= 109`

**My Solutions:**

* 方法1：brute force，对nums的每一个数，看有没有比Ta +1和-1的数。
* 方法2：先排序，再traverse每一个数。Time: O\(nlgn\)
* 方法3：把nums的每个数存在hashset里。在traverse hashset的时候，把每个数的+1和-1都找一遍。每次找到一个数，都把Ta从set里删去。Time: O\(n\)

```text
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums == null || nums.length == 0)   return 0;
        
        HashSet<Integer> set = new HashSet<>();
        for (int i : nums) set.add(i);
        
        int res = 0;
        
        for (int i : nums) {
            if (set.contains(i)) {
                set.remove(i);
                
                int pre = i - 1;
                int next = i + 1;
                while (set.contains(pre)) {
                    set.remove(pre);
                    pre--;
                }
                while (set.contains(next)) {
                    set.remove(next);
                    next++;
                }
                res = Math.max(res, next - pre - 1);
            }
            
        }
        return res;
        
    }
}
```

