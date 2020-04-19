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

建立字母频率count\[ \]，和t长度total，当total为零时，slide window

```
class Solution { public String minWindow(String s, String t) {   if (t.length() > s.length()) return "";     int[] count = new int[128];     for (char c : t.toCharArray()) count[c]++; //保存char出现的次数            int start = 0, total = t.length(), lenS = s.length(), min = lenS + 1;    for (int i = 0, j = 0; i < s.length(); i++) {        if (count[s.charAt(i)] > 0) { //如果此char在t中，total减一            total--;        }        count[s.charAt(i)]--; //无论如何此char的次数减一        while (total == 0) {            if (i - j + 1 < min) {                min = i - j + 1;                start = j;            }            count[s.charAt(j)]++; //需要右移sliding window，所以先把开头的次数加一            if (count[s.charAt(j)] > 0) total++; //count[j] > 0 说明此char在t中,total加一            j++;        }    }    return min == lenS + 1 ? "" : s.substring(start, start + min); }
```

