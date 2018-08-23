# Two Sum III - Data structure design

**Two Sum III - Data structure design**

Design and implement a TwoSum class. It should support the following operations: add and find.

`add(input)` – Add the number input to an internal data structure.

`find(value)` – Find if there exists any pair of numbers which sum is equal to the value.

For example, `add(1); add(3); add(5); find(4)->true; find(7)->false`

_**My Solutions：**_

记录input时也要记录个数，比如6可以由两个3，3构成

方法1：add优先

add：用hashtable储存key和个数，add时数字个数+1。Time=O\(1\)

find：用hashtable依次寻找pair。Time=O\(n\)

Space=O\(n\)

```text
public class TwoSum {
	private HashMap<Integer, Integer> elements = new HashMap<Integer, Integer>();
 
	public void add(int number) {
		if (elements.containsKey(number)) {
			elements.put(number, elements.get(number) + 1);
		} else {
			elements.put(number, 1);
		}
	}
 
	public boolean find(int value) {
		for (Integer i : elements.keySet()) {
			int target = value - i;
			if (elements.containsKey(target)) {
				if (i == target && elements.get(target) < 2) {
					continue;
				}
				return true;
			}
		}
		return false;
	}
}
```

方法2：add优先，不使用hashtable

add: O\(1\); find: O\(nlgn\); Space: O\(n\)

```text
public class TwoSum {

    ArrayList<Integer> nums = new ArrayList<>();
    
    public void add(int number) {
        nums.add(number);
    }

    public boolean find(int value) {
        Collections.sort(nums);
        for (int i = 0, j = nums.size() - 1; i < j;) {
            if (nums.get(i) + nums.get(j) == value) {
                return true;
            } else if (nums.get(i) + nums.get(j) < value) {
                i++;
            } else {
                j--;
            }
        }
        return false;
    }
}

```

方法3：find优先

用一个nums储存数字和一个sums储存所有可能的总和

add：每加入一个数字，sums加上这个数字和之前的所有数字之和.Time=O\(n\)

find：检查sums里是否有target. Time=O\(1\)

Space: O\(n\)





