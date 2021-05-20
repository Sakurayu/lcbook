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

* \*\*\*\*[**N-ary Tree Preorder**](https://leetcode.com/problems/n-ary-tree-preorder-traversal/)\*\*\*\*

```text
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val,List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {

    // 方法1
    public List<Integer> preorder(Node root) {
//         List<Integer> list = new ArrayList<>();
//         traverse(list, root);
//         return list;
//     }
    
//     public void traverse(List<Integer> list, Node root) {
//         if (root == null) return;
//         list.add(root.val);
            // 从前往后加children
//         for (int i = 0; i < root.children.size(); i++) {
//             traverse(list, root.children.get(i));
//         }
        
        // 方法2
        List<Integer> list = new ArrayList<>();
        Stack <Node> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            Node node = stack.pop();
            if (node != null) {
                list.add(node.val);
                // 从后往前加children
                for (int i = node.children.size() - 1; i >= 0; i--) {
                    stack.push(node.children.get(i));
                }
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
            list.addFirst(n.val); //加到list最前，或者用add(0, node.val)。这样现在的数字将来会在list的最后面。
            if (n.left != null) stack.push(n.left); //stack 先左后右 ==> 因为用addFirst,  list最终结果为先左后右
            if (n.right != null) stack.push(n.right);
        }
        return list;
    }
}
```

* \*\*\*\*[**N-ary Tree Postorder**](https://leetcode.com/problems/n-ary-tree-postorder-traversal/)\*\*\*\*

```text
class Solution {
    public List<Integer> postorder(Node root) {
        LinkedList<Integer> list = new LinkedList<Integer>();
        // 方法1
        if (root == null) return list;
//         traverse(list, root);
//         return list;
//     }
    
//     public void traverse(List<Integer> list, Node root) {
//         if (root == null) return;
        
//         for (int i = 0; i < root.children.size(); i++) {
//             traverse(list, root.children.get(i));
//         }
        
//         list.add(root.val);
//     }
        
        // 方法2
        Stack<Node> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            Node n = stack.pop();
            list.addFirst(n.val);
            for (Node node : n.children) {
                stack.push(node);
            }
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

1。 方法1：iterative bfs - queue 先进先出

```text
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
    
        List<List<Integer>> list = new LinkedList<>();
        if (root == null) return list;
        // queue需要用linked list
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int size = queue.size(); //必须要先把size存下来，因为在for loop里，每次都要poll，影响queue的size
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
        
        // 每一层height应该有一个对应list的element，储存这一层的所有children的值
        // 因此，当height >= list.size()时，在list里加入一个空的新元素。
        if (height >= list.size()) list.add(new LinkedList<Integer>());
        
        // 每一个root的值，应该加入它所在的list的元素里，元素的index是height。
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

* \*\*\*\*[**N-ary Tree Levelorder**](https://leetcode.com/problems/n-ary-tree-level-order-traversal/)\*\*\*\*

```text
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> list = new ArrayList<>();
        if (root == null) return list;
        
        // 方法1
//         Queue<Node> q = new LinkedList<>();
//         q.offer(root);
        
//         while (!q.isEmpty()) {
//             int size = q.size();
//             List<Integer> level = new ArrayList<>();
//             for (int i = 0; i < size; i++) {
//                 Node node = q.poll();
//                 level.add(node.val);
//                 for (Node n : node.children) {
//                     q.offer(n);
//                 }
//             }
//             list.add(level);
//         }
        helper(list, root, 0);
        return list;
    }
    
    // 方法2
    private void helper(List<List<Integer>> list, Node root, int height) {
        if (root == null) return;
        if (height >= list.size()) list.add(new LinkedList<Integer>());
        list.get(height).add(root.val);
        for (Node node : root.children) {
            helper(list, node, height + 1);
        }
    }
}
```

