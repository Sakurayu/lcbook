# Roman/Integer

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```text
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

\*\*\*\*[ **13. Roman to Integer**](https://leetcode.com/problems/roman-to-integer/description/)\*\*\*\*

**Example:**

```text
Input: "LVIII"
Output: 58
Explanation: C = 100, L = 50, XXX = 30 and III = 3.
```

_**My solutions：**_

```text
public class Solution {
     public int romanToInt(String s) {
	    if (s == null || s.length()==0) return 0;
	    
	    Map<Character, Integer> m = new HashMap<Character, Integer>();
	    m.put('I', 1);
	    m.put('V', 5);
	    m.put('X', 10);
	    m.put('L', 50);
	    m.put('C', 100);
	    m.put('D', 500);
	    m.put('M', 1000);

	    int length = s.length();
	
	    int result = m.get(s.charAt(length - 1));
	
	    // 从倒数第二位开始,如果右边一位比左边一位小或相等，说明可以直接加上当前位
        // 不然就是'IX'的情况，需要减去当前位
       for (int i = length - 2; i >= 0; i--) {
	        if (m.get(s.charAt(i + 1)) <= m.get(s.charAt(i))) {
	            result += m.get(s.charAt(i));
	        } else {
	            result -= m.get(s.charAt(i));
	        }
	    }
	    return result;
	}
}
```

\*\*\*\*[ **12. Integer to Roman**](https://leetcode.com/problems/integer-to-roman/description/)\*\*\*\*

_**My solutions：**_

把所有的可能数字按照10以下，10~90， 100~900， 1000~3000分别存在几个array里。需要转换的数字按照 / 的余数分别去取array里的数字

```text
public class Solution {
    public String intToRoman(int num) {
        String M[] = {"", "M", "MM", "MMM"};
        String C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        String X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        String I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};   
        return M[num/1000] + C[(num % 1000) /100] + X[(num % 100) /10] + I[num % 10];
    }
}
```



