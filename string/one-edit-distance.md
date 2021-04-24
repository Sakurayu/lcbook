# One Edit Distance

**One Edit Distance**

Given two strings S and T, determine if they are both one edit distance apart.

_**My Solutions:**_

如果S和T长度相差大于1，直接返回false；

如果长度相等，检查是否最多有一次字符不同；

如果长度相差1，说明有一次删除或插入字符。找到第一个不相符的位置，如果较长字串在这个位置之后的部分和较短字串从此位开始都一致，则返回true。

