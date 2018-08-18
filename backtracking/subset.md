# Subset

[ **78. Subsets**](https://leetcode.com/problems/subsets/description/)

Given a set of **distinct** integers, _nums_, return all possible subsets \(the power set\).

**Note:** The solution set must not contain duplicate subsets.

**Example:**

```text
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

**My Solutions:**

注意dfs的for loop中，i=start，只能从前往后找

```text
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        Arrays.sort(nums);
        dfs(list, new ArrayList<>(), nums, 0);
        return list;
    }
    
    private void dfs(List<List<Integer>> list, List<Integer> temp, int[] nums, int start) {
        list.add(new ArrayList<>(temp));
        for (int i = start; i < nums.length; i++) {
            temp.add(nums[i]);
            dfs(list, temp, nums, i + 1);
            temp.remove(temp.size() - 1);
        }
    }
}
```

方法2：非递归，按照组合的思想，一个数字都没有的时候是空集；有一个数字，则这个数字+空集是一个新集合。e.g. \[1,2,3\]

一开始放空集【】，之后是【】，【1】。再之后是【】，【1】，【2】，【1，2】......

```text
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        list.add(new ArrayList<>()); //空集
        for (int n : nums) { //从nums中取出每一个元素
            int size = list.size();
            for (int i = 0; i < size; i++) {
                List<Integer> temp = new ArrayList<>(list.get(i)); //temp是list中已有的
                temp.add(n); //把新元素加入temp
                list.add(temp); //新temp加入list中
            }
        }
        return list;
    }
```

[ **90. Subsets II**](https://leetcode.com/problems/subsets-ii/description/)

Given a collection of integers that might contain duplicates, _**nums**_, return all possible subsets \(the power set\).

**Note:** The solution set must not contain duplicate subsets.

**Example:**

```text
Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

**My Solutions:**

和上题类似，多增加一步跳过duplicates

```text
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        Arrays.sort(nums);
        dfs(list, new ArrayList<>(), nums, 0);
        return list;
    }
    
    public void dfs(List<List<Integer>> list, List<Integer> temp, int[] nums, int start) {
        
        list.add(new ArrayList<>(temp));
        
        for (int i = start; i < nums.length; i++) {
            if (i > start && nums[i] == nums[i - 1]) continue; //跳过duplicates
            temp.add(nums[i]);
            dfs(list, temp, nums, i + 1);
            temp.remove(temp.size() - 1);
        }
    }
}
```

