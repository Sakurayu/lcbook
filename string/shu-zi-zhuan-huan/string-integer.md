# String/Integer

\*\*\*\*[ **8. String to Integer \(atoi\)**](https://leetcode.com/problems/string-to-integer-atoi/description/)\*\*\*\*

_**My Solutions:**_

```text
public class Solution {
    public int myAtoi(String str) {
        
        if (str == null || str.length() == 0) return 0;
 		str = str.trim();
		int i = 0, ans = 0, sign = 1;
		if (str.charAt(i) == '+' || str.charAt(i) == '-')
			sign = (str.charAt(i++) == '+' ? 1 : -1);
		for (; i < str.length(); i++) {
			int tmp = str.charAt(i) - '0';
			if (tmp < 0 || tmp > 9)
				break;
			if (ans > Integer.MAX_VALUE / 10
					|| (ans == Integer.MAX_VALUE / 10 && Integer.MAX_VALUE % 10 < tmp))
				return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
			else
				ans = ans * 10 + tmp;
		}
		return sign * ans;
    }
}
```

