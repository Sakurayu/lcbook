# Tree Traversal

     1

   /  \

 2     3

/ \

4  5

## DFS

Time: O\(n\); Space: stack: O\(n\)

* [**Preorder**](https://leetcode.com/problems/binary-tree-preorder-traversal/description/)\(root, left, right\): 1, 2, 4, 5, 3 中左右

```text
public ArrayList<Integer> traversal(Node root) {
    ArrayList<Integer> list = new ArrayList<>();
    if (root == null) return list;
    return helper(root, lits);
}

public ArrayList<Integer> preOrderHelper(Node root, ArrayList<Integer> list) {
    if (node != null) {
        list.add(node.val);
        preOrderHelper(noot.left, list); 
        preOrderHelper(root.right, list); 
    }
    return list;
}   
```

```text
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> list = new LinkedList<>();
        Stack <TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            if (node != null) {
                list.add(node.val);
                stack.push(node.right); //stack先右后左==> list先左后右
                stack.push(node.left);
            }
        }
        return list;
    }
}
```

* [**Inorder**](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)\(left, root, right\): 4, 2, 5, 1, 3 左中右

```text
public ArrayList<Integer> inOrderHelper(Node root, ArrayList<Integer> list) {
    if (node != null) {
        inOrderHelper(noot.left, list); 
        list.add(node.val);
        inOrderHelper(root.right, list); 
    }
    return list;
}   
```

```text
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new LinkedList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode node = root;
        while (node != null || !stack.isEmpty()) {
            while (node != null) {
                stack.push(node);
                node = node.left;     
            }
            node = stack.pop();
            list.add(node.val);
            node = node.right;
        }
        return list;
    }
}
```

* [**Postorder**](https://leetcode.com/problems/binary-tree-postorder-traversal/description/)\(left, right, root\): 4, 5, 2, 3, 1 左右中

```text
public ArrayList<Integer> postOrderHelper(Node root, ArrayList<Integer> list) {
    if (node != null) {
        postOrderHelper(noot.left, list); 
        postOrderHelper(root.right, list);
        list.add(node.val);
        
    }
    return list;
} 
```

```text
class Solution {
    public Linkedist<Integer> postorderTraversal(TreeNode root) {
        LinkedList<Integer> list = new LinkedList<>(); //List 没有addFirst的method
        Stack<TreeNode> stack = new Stack<>();
        if (root == null) return list;
        stack.push(root);
        
        while (!stack.isEmpty()) {
            TreeNode n = stack.pop();
            list.addFirst(n.val); //加到list最前，或者用add(0, node.val)
            if (n.left != null) stack.push(n.left); //stack 先左后右 ==> 因为用addFirst,  list最终结果为先左后右
            if (n.right != null) stack.push(n.right);
        }
        return list;
    }
}
```



## BFS

* [**Levelorder**](https://leetcode.com/problems/binary-tree-level-order-traversal/description/): 1, 2, 3, 4, 5

For example:  
Given binary tree `[3,9,20,null,null,15,7]`,

```text
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```text
[
  [3],
  [9,20],
  [15,7]
]
```

1。 方法1：iterative bfs - queue

```text
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
    
        List<List<Integer>> list = new LinkedList<>();
        if (root == null) return list;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> level = new LinkedList<>();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                level.add(node.val);
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            list.add(level);
        }
        return list;
```

2。 方法2： recursive dfs

```text
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> list = new LinkedList<>();
        if (root == null) return list;
        helper(list, root, 0);
        return list;
    }
    
    private void helper(List<List<Integer>> list, TreeNode root, int height) {
        if (root == null) return;
        if (height >= list.size()) list.add(new LinkedList<Integer>());
        list.get(height).add(root.val);
        helper(list, root.left, height + 1);
        helper(list, root.right, height + 1);
    }
}
```

* [**Levelorder II**](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/description/)

For example:  
Given binary tree `[3,9,20,null,null,15,7]`,

```text
    3
   / \
  9  20
    /  \
   15   7
```

return its bottom-up level order traversal as:

```text
[
  [15,7],
  [9,20],
  [3]
]
```

**My Solutions:**

1. BFS: 和level order类似，但level加入list时，用 list.add\(0, level\), 或者最后reverse list
2. DFS：和level order类似，但在helper里，把 new LinkedList&lt;&gt;\(\) 加入list时，用 list.add\(0, new LinkedList&lt;Integer&gt;\(\)\), 或者最后 Collection.reverse\(list\)

* [**Zigzag Levelorder**](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/description/)

For example:  
Given binary tree `[3,9,20,null,null,15,7]`,

```text
    3
   / \
  9  20
    /  \
   15   7
```

return its zigzag level order traversal as:

```text
[
  [3],
  [20,9],
  [15,7]
]
```

**My Solutions:**

DFS：和level order类似，但在helper里，多一个判断条件

```text
if (height % 2 == 0) list.get(height).add(root.val);
else list.get(heigth).add(0, root.val);
```

