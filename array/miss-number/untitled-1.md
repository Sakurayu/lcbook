# 448. Find All Numbers Disappeared in an Array

\*\*\*\*[ **448. Find All Numbers Disappeared in an Array**](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/description/)\*\*\*\*

Given an array of integers where 1 ≤ a\[i\] ≤ n \(n = size of array\), some elements appear twice and others appear once.

Find all the elements of \[1, n\] inclusive that do not appear in this array.

Could you do it without extra space and in O\(n\) runtime? You may assume the returned list does not count as extra space.

**Example:**

```text
Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```

_**My Solutions:**_

除了类似268中，sort和hash的办法，还可以利用index

方法3：

Time: O\(n\); Space: O\(1\)

```text
public class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        
        List<Integer> res = new ArrayList<Integer>();
        
        for (int i = 0; i < nums.length; i++) {
            int val = Math.abs(nums[i]) - 1; //遇到一个数字时，把它的绝对值转换成index
            if (nums[val] > 0) nums[val] = -nums[val]; //如果这个index上的数字是正数，把这个数换成负数
        }
        
        //在这一步结束之后，所有只出现一次的index上的数字是负数
        //index上是正数的数字说明没有正负颠倒过，也就是这个数是disappear的
        
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > 0) res.add(i + 1);
        }
        
        return res;
        
    }
}
```

