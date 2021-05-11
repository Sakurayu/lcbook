# 76. Minimum Window Substring

 [**76. Minimum Window Substring**](https://leetcode.com/problems/minimum-window-substring/description/)

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O\(n\).

**Example:**

```text
Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
```

**Note:**

* If there is no such window in S that covers all characters in T, return the empty string `""`.
* If there is such window, you are guaranteed that there will always be only one unique minimum window in S.

_**My Solutions:**_

建立t中字母频率count\[ \]。把t的长度记做total，每次在s中遇见t中的字母，total减一。当total为零时，说明t中的所有字母都已经在这个window中找到，可以slide window。

用i记录sliding window的末端，j记录sliding window的首位。

```
class Solution {
    public String minWindow(String s, String t) {
        if (t.length() > s.length()) return "";
        int[] count = new int[128];
        for (char c : t.toCharArray()) count[c]++; //保存t中间每个char出现的次数，如果一个char没有出现，自动记为0
        
        int start = 0, total = t.length(), lenS = s.length(), min = lenS + 1;
        
        for (int i = 0, j = 0; i < s.length(); i++) {
            if (count[s.charAt(i)] > 0) { //如果此char在t中，total减一
                total--;
            }
            count[s.charAt(i)]--; //无论如何此char的在count中的次数减一
            while (total == 0) { // 只要total==0，说明t的字母都在已有的window里，可以继续往右slide window，知道total>=0, 需要的字母不再包含在window里
                if (i - j + 1 < min) { // 只有找到一个更小的window时
                    min = i - j + 1; // 更新min
                    start = j; // 更新记录window起点的start
                }
                count[s.charAt(j)]++; //需要右移sliding window，所以先把开头字母在count里的次数加一
                if (count[s.charAt(j)] > 0) total++; //count[j] > 0 说明此char在t中。由于我们要slide window，window中不再有这个字母，所以total需要++
                j++;
            }
        }
        
        return min == lenS + 1 ? "" : s.substring(start, start + min); 
    }
}
```

