# 213. House Robber II

 [**213. House Robber II**](https://leetcode.com/problems/house-robber-ii/description/)

 Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```text
Input: [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),
             because they are adjacent houses.
```

**Example 2:**

```text
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

_**My Solutions:**_

和上题不同的地方是有环，所有要考虑两种情况：从第一个开始rob，rob到倒数第二个；从第二个开始rob，rob到倒数第一个

```text
class Solution {
    public int rob(int[] nums) {
        if (nums.length == 1) return nums[0];
        return Math.max(helper(nums, 0, nums.length - 2), helper(nums, 1, nums.length - 1));
        
    }
    
    public int helper(int[] nums, int lo, int hi) {
        int profit = 0;
        int lastP = 0;
        
        for (int i = lo; i <= hi; i++) {
            int temp = lastP;
            lastP = profit;
            profit = Math.max(profit, nums[i] + temp);
        }
        return profit;
    
        
    }
}
```

