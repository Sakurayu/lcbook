# Depth & Diameter

[**Max. Depth**](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)

```text
public class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```



\*\*\*\*[**Maximum Depth of N-ary Tree**](https://leetcode.com/problems/maximum-depth-of-n-ary-tree/description/)\*\*\*\*

```text
class Solution {
    public int maxDepth(Node root) {
        if (root == null) return 0;
        int res = 0;
        
        //recursive 
        // for (Node node : root.children) {
        //     res = Math.max(res, maxDepth(node));
        // }
        // return res + 1;
        
        //iterative
        Queue<Node> q = new LinkedList<>();
        q.add(root);
        int count = 0;
        while(!q.isEmpty()) {
            res++;
            count = q.size();
            for (int i = 0; i < count; i++) {
                Node node = q.poll();
                for (Node n : node.children) {
                    q.add(n);
                }
            }
        }
        return res;
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



 [**543. Diameter of Binary Tree**](https://leetcode.com/problems/diameter-of-binary-tree/description/)\*\*\*\*

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the **longest** path between any two nodes in a tree. This path may or may not pass through the root.

**Example:**

```text
          1
         / \
        2   3
       / \     
      4   5    
```

Return **3**, which is the length of the path \[4,2,1,3\] or \[5,2,1,3\].

**Note:** The length of path between two nodes is represented by the number of edges between them.

  
_**My solutions：**_

```text
class Solution {
    
    int ans;
    
    public int diameterOfBinaryTree(TreeNode root) {
        if (root == null) return 0;
        di(root);
        return ans;
    }
    
    public int di(TreeNode root) {
        if (root == null) return 0;
        int left = di(root.left);
        int right = di(root.right);
        ans = Math.max(ans, left + right); //diameter不加1
        return Math.max(left, right) + 1; //只可以在left和right path中选择一条路，所以需要+1，加上path结束时的那个node
    }
}
```



