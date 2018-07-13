# Depth

[**Max. Depth**](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)

```text
public class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```

[**Min. Depth**](https://leetcode.com/problems/minimum-depth-of-binary-tree/description/)

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

**Note:** A leaf is a node with no children.

**Example:**

Given binary tree `[3,9,20,null,null,15,7]`,

```text
    3
   / \
  9  20
    /  \
   15   7
```

return its minimum depth = 2.

_**My Solutions:**_

```text
public class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        if (root.left != null && root.right != null) { //has both children, return the min one
            return Math.min(minDepth(root.left), minDepth(root.right)) + 1;
        } else { //only has left/right child, return the max one
            return Math.max(minDepth(root.left), minDepth(root.right)) + 1;
        }
    }
}
```

