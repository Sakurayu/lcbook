# 135. Candy

135. Candy



There are `n` children standing in a line. Each child is assigned a rating value given in the integer array `ratings`.

You are giving candies to these children subjected to the following requirements:

* Each child must have at least one candy.
* Children with a higher rating get more candies than their neighbors.

Return _the minimum number of candies you need to have to distribute the candies to the children_.

**Example 1:**

```text
Input: ratings = [1,0,2]
Output: 5
Explanation: You can allocate to the first, second and third child with 2, 1, 2 candies respectively.
```

**Example 2:**

```text
Input: ratings = [1,2,2]
Output: 4
Explanation: You can allocate to the first, second and third child with 1, 2, 1 candies respectively.
The third child gets 1 candy because it satisfies the above two conditions.
```

**Constraints:**

* `n == ratings.length`
* `1 <= n <= 2 * 104`
* `0 <= ratings[i] <= 2 * 104`

_**My Solutions:**_

从前到后，从后到前，走两遍。在从后到前的那一遍，顺便把sum求出来。

```text
class Solution {
    public int candy(int[] ratings) {
        if (ratings == null  || ratings.length == 0) return 0;
        int len = ratings.length;
        if (len == 1) return 1;
        
        int[] candy = new int[len];
        candy[0] = 1;
    
        for (int i = 1; i < len; i++) {
            if (ratings[i] > ratings[i - 1]) candy[i] = candy[i - 1] + 1;
            else candy[i] = 1;
        }
        
        int sum = candy[len - 1];
        
        for (int i = len - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) candy[i] = Math.max(candy[i], candy[i + 1] + 1);
            sum += candy[i];
        }
        return sum;
    }
}
```

