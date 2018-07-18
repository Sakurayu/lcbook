# 581. Shortest Unsorted Continuous Subarray

\*\*\*\*[**581. Shortest Unsorted Continuous Subarray** ](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/description/)\*\*\*\*

Given an integer array, you need to find one **continuous subarray** that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.

You need to find the **shortest** such subarray and output its length.

**Example 1:**  


```text
Input: [2, 6, 4, 8, 10, 9, 15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
```

**Note:**  


1. Then length of the input array is in range \[1, 10,000\].
2. The input array may contain duplicates, so ascending order here means **&lt;=**.

_**My Solutions:**_

方法1：先sort array，然后依次对照，找出不相同的数字

时间 & 空间：O（nlgn）

方法2：用stack储存index。先从左往右，如果新元素比现有元素小，则pop出所有比新元素大的元素index，用int left把pop出的最小index记下来。同样方法，从右往左，记下pop出的最大index。两者之间就是unsorted

```text
class Solution {
    public int findUnsortedSubarray(int[] nums) {
        if (nums == null || nums.length <= 1) return 0;
        
        Stack<Integer> stack = new Stack<>();
        int left = nums.length - 1, right = 0;
        
        for (int i = 0; i < nums.length; i++) {
            while (!stack.isEmpty() && nums[stack.peek()] > nums[i]) {
                left = Math.min(left, stack.pop());
            }
            stack.push(i);
        }
        
        stack.clear();
        
        for (int i = nums.length - 1; i >= 0; i--) {
            while (!stack.isEmpty() && nums[stack.peek()] < nums[i]) {
                right = Math.max(right, stack.pop());
            }
            stack.push(i);
        }
        
        return right <= left ? 0 : right - left + 1;
        
        
    }
}
```

时间 & 空间 ：O（n）

方法3：正确的排列是从左往右依次增大。因此，从右往左，找到最后一个变大的点，就是unsort的起点。从左往右，找到最后一个变小的点，就是unsort的终点。unsorted的部分就是两者之间

时间：O（n）；空间：O（1）

```text
class Solution {
    
    // find the dropping point at the begin and the increasing point at the end
    public int findUnsortedSubarray(int[] nums) {
        
        // find the begin, from right to left, find the last increase point
        int begin = -1;
        int min = nums[nums.length - 1];
        for (int i=nums.length-2; i>=0; i--) {
            min = Math.min(min, nums[i]);
            if (nums[i] > min) {
                begin = i;
            }
        }
        
        // find the end, from left to right, find the last drop point
        int end = -1;
        int max = nums[0];
        for (int i=1; i<nums.length; i++) {
            max = Math.max(max, nums[i]);
            if (nums[i] < max) {
                end = i;
            }
        }
        
        if (begin == -1 && end == -1) {
            return 0;
        } else {
            return end - begin + 1;
        }
    }
}
```





