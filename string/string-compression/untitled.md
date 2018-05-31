# 38. Count and Say

 [**38. Count and Say**](https://leetcode.com/problems/count-and-say/description/)

The count-and-say sequence is the sequence of integers with the first five terms as following:

```text
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

`1` is read off as `"one 1"` or `11`.  
`11` is read off as `"two 1s"` or `21`.  
`21` is read off as `"one 2`, then `one 1"` or `1211`.  


Given an integer n, generate the nth term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

**Example 1:**

```text
Input: 1
Output: "1"
```

**Example 2:**

```text
Input: 4
Output: "1211"
```

_**My Solutions:**_

每一层都要用一次string compression

```text
class Solution {
    public String countAndSay(int n) {
        String res = "1";
        if (n == 1) return res;
        for (int i = 1; i < n; i++) {
            res = helper(res);
        }
        return res;
    }
    
    public String helper(String s) {
        char[] arr = s.toCharArray();
        int count = 1;
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            if (i == s.length() - 1 || arr[i] != arr[i + 1]) { //has to check i == s.length() - 1 first to make sure no index out of range
                sb.append(count);
                sb.append(arr[i]);
                count = 1;
            } else {
                count++;
            }
        }
        return sb.toString();
    } 
}
```

