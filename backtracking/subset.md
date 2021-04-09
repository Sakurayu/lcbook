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

_**My Solutions:**_

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
        list.add(new ArrayList<>(temp)); //先放入之前的
        for (int i = start; i < nums.length; i++) {
            temp.add(nums[i]); //在之前的放入新元素
            dfs(list, temp, nums, i + 1);
            temp.remove(temp.size() - 1); //回头的时候，需要去掉temp里最后加入的元素
        }
    }
}
```

方法2：非递归，按照组合的思想，一个数字都没有的时候是空集；有一个数字，则这个数字+空集是一个新集合。因此，每循环到一个新元素，就把之前已经加入的所有list再加上这个元素，再加入list of list

e.g. 【1，2，3】

一开始list里只有空集【】；

第一个n是1，n=1，size=1，内for loop循环结束一次之后list是【】，【1】；内for loop循环第二次之后list是【】，【1】，【2】，【1，2】

第二个n是2，n=2，size=4，内for loop循环一次结束后，list是【】，【1】，【2】，【1，2】，【3】；内for loop循环第二次后list是【】，【1】，【2】，【1，2】，【3】，【1，3】；第三次后是【】，【1】，【2】，【1，2】，【3】，【1，3】，【2，3】；第四次后是【】，【1】，【2】，【1，2】，【3】，【1，3】，【2，3】，【1，2，3】

```text
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> list = new ArrayList<>();
        list.add(new ArrayList<>()); //空集
        for (int n : nums) { //从nums中取出每一个元素
            int size = list.size();
            for (int i = 0; i < size; i++) {
                List<Integer> temp = new ArrayList<>(list.get(i)); //temp是list中已有的数组
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

_**My Solutions:**_

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

