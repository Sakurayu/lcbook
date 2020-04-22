# Leftmost Column with at Least a One

Leftmost Column with at Least a One

_\(This problem is an **interactive problem**.\)_

A binary matrix means that all elements are `0` or `1`. For each **individual** row of the matrix, this row is sorted in non-decreasing order.

Given a row-sorted binary matrix binaryMatrix, return leftmost column index\(0-indexed\) with at least a `1` in it. If such index doesn't exist, return `-1`.

**You can't access the Binary Matrix directly.**  You may only access the matrix using a `BinaryMatrix` interface:

* `BinaryMatrix.get(x, y)` returns the element of the matrix at index `(x, y)` \(0-indexed\).
* `BinaryMatrix.dimensions()` returns a list of 2 elements `[m, n]`, which means the matrix is `m * n`.

Submissions making more than `1000` calls to `BinaryMatrix.get` will be judged _Wrong Answer_.  Also, any solutions that attempt to circumvent the judge will result in disqualification.

For custom testing purposes you're given the binary matrix `mat` as input in the following four examples. You will not have access the binary matrix directly.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-5.jpg)

```text
Input: mat = [[0,0],[1,1]]
Output: 0
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-4.jpg)

```text
Input: mat = [[0,0],[0,1]]
Output: 1
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-3.jpg)

```text
Input: mat = [[0,0],[0,0]]
Output: -1
```

**Example 4:**

![](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-6.jpg)

```text
Input: mat = [[0,0,0,1],[0,0,1,1],[0,1,1,1]]
Output: 1
```

**Constraints:**

* `m == mat.length`
* `n == mat[i].length`
* `1 <= m, n <= 100`
* `mat[i][j]` is either `0` or `1`.
* `mat[i]` is sorted in a non-decreasing way.

Hint 1: \(Binary Search\) For each row do a binary search to find the leftmost one on that row and update the answer.

Time: O\(m \* lgn\) 因为一行有n列，binary search一行需要lgn，重复m行

Hint 2: \(Optimal Approach\) Imagine there is a pointer p\(x, y\) starting from top right corner. p can only move left or down. If the value at p is 0, move down. If the value at p is 1, move left. Try to figure out the correctness and time complexity of this algorithm.

_**My Solutions:**_

根据每一行一定是递增的这个特点，可以知道从右上角的点开始，如果碰到1，就可以左移直到碰到0为止；如果碰到0，就可以下移直到碰到1为止。一直移动直到出了matrix的边界。

Time: O\(max\(m, n\)\) 最多查看m或者n之中最大值的次数

```text
/**
 * // This is the BinaryMatrix's API interface.
 * // You should not implement it, or speculate about its implementation
 * interface BinaryMatrix {
 *     public int get(int x, int y) {}
 *     public List<Integer> dimensions {}
 * };
 */

class Solution {
    public int leftMostColumnWithOne(BinaryMatrix binaryMatrix) {
        List<Integer> dimension = binaryMatrix.dimensions();
        int m = dimension.get(0), n = dimension.get(1);
        int i = 0, j = n - 1;
        int res = -1;
        
        while (i < m && j >= 0) {
            if (binaryMatrix.get(i, j) == 0) i++;
            else {
                res = j;
                j--;
            }
        }
        return res;
    }
}
```

