# Array 模板

```text
class Solution {
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) return -1;
        
        int left = 0, right = nums.length - 1;
        
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid; //直接返回index
            else if (nums[mid] > target) right = mid;
            else left = mid;
        }
        return -1;        
    }
}
```

注意：用 left + 1 &lt; right是为了防止出现left == right，跳不出while循环的情况。

比如\[1,3,4\]，寻找2。第一次left=0，right=2，mid=3，right变成1。第二次left=0，right=1，mid=0，left变成1。如果用left&lt;=right，则跳不出这个循环。

**变形1：有重复数字，找到first position of target**

```text
class Solution {
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) return -1;
        
        int left = 0, right = nums.length - 1;
        
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) right = end; //不直接返回，继续向前检查
            else if (nums[mid] > target) right = mid;
            else left = mid;
        }
                
        if (target == nums[left]) return left; //先检查前面
        if (target == nums[right]) return right;
        
        return -1;        
    }
}
```

**变形2：有重复数字，找到last position of target**

```text
class Solution {
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) return -1;
        
        int left = 0, right = nums.length - 1;
        
        while (left + 1 < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) left = end; //不直接返回，继续向后检查
            else if (nums[mid] > target) right = mid;
            else left = mid;
        }
                
        if (target == nums[right]) return right; //先检查后面
        if (target == nums[left]) return left; 
        
        return -1;        
    }
}
```

