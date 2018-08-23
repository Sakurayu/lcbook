# Climb Stairs

 [**70. Climbing Stairs**](https://leetcode.com/problems/climbing-stairs/description/)\*\*\*\*

You are climbing a stair case. It takes _n_ steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note:** Given _n_ will be a positive integer.

**Example 1:**

```text
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**

```text
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

_**My Solutions:**_

假设梯子有n层，那么如何爬到第n层呢，因为每次只能爬1或2步，那么爬到第n层的方法要么是从第n-1层一步上来的，要不就是从n-2层2步上来的，所以：

dp\[n\] = dp\[n-1\] + dp\[n-2\]

```text
class Solution {
    public int climbStairs(int n) {
        if (n <= 1) return 1;
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```

引申一下，如果是可以走1，2，3，4步呢？

1：1种解法

2：2种解法

3：4种解法

4：8种解法

5：15种解法

dp\[i\]=dp\[i-1\]+dp\[i-2\]+dp\[i-3\]+dp\[i-4\]



 [**746. Min Cost Climbing Stairs**](https://leetcode.com/problems/min-cost-climbing-stairs/description/)\*\*\*\*

On a staircase, the `i`-th step has some non-negative cost `cost[i]` assigned \(0 indexed\).

Once you pay the cost, you can either climb one or two steps. You need to find minimum cost to reach the top of the floor, and you can either start from the step with index 0, or the step with index 1.

**Example 1:**

```text
Input: cost = [10, 15, 20]
Output: 15
Explanation: Cheapest is start on cost[1], pay that cost and go to the top.
```

**Example 2:**

```text
Input: cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
Output: 6
Explanation: Cheapest is start on cost[0], and only step on 1s, skipping cost[3].
```

**Note:**

1. `cost` will have a length in the range `[2, 1000]`.
2. Every `cost[i]` will be an integer in the range `[0, 999]`.

  
_**My Solutions:**_  
因为每次只能跳一步或两步，所以想要跳到i层，只能从i-2起跳+cost【i-2】，或者i-1起跳+cost【i-1】，取两者中较小值。因为一开始可以站在0或者1上，所以设置这两个dp【】=0，不需要加上cost；这两个数另外的位置起跳都需要加上位置的cost。dp要比cost的length多一，是因为必须要跳出最后一格

```text
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int n = cost.length + 1;
        int[] dp = new int[n];
        dp[0] = 0;
        dp[1] = 0;
        for (int i = 2; i < n; i++) {
            dp[i] = Math.min(dp[i - 2] + cost[i - 2], dp[i - 1] + cost[i - 1]);
        }
        return dp[n - 1];
    }
}
```

