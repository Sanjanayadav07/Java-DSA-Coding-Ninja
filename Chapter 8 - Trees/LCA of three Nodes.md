# 🌳 LCA of Three Nodes in Binary Tree
## 📌 Problem Statement
- Given the root of a binary tree and three node values.
- Find the Lowest Common Ancestor (LCA) of the three nodes.
- The LCA is the lowest node in the tree that has all three nodes as descendants.

---
## 🧠 Approach
- First, find LCA of first two nodes using standard binary tree LCA logic.
- Then, find LCA of the result and the third node.
- This works because:
  - LCA(a, b, c) = LCA(LCA(a, b), c)
- Steps:
- Write a helper function to find LCA of two nodes.
- Use it twice:
   - firstLCA = LCA(node1, node2)
   - Final answer = LCA(firstLCA, node3)
---
## ⏱️ Complexity Analysis
- Time Complexity: O(N)
- Space Complexity: O(N)
   - (Recursive call stack in worst case)
---
## 💻 Code
```
public class Solution {

    // LCA of two nodes
    private static BinaryTreeNode<Integer> lca(
            BinaryTreeNode<Integer> root, int a, int b) {

        if (root == null)
            return null;

        if (root.data == a || root.data == b)
            return root;

        BinaryTreeNode<Integer> left = lca(root.left, a, b);
        BinaryTreeNode<Integer> right = lca(root.right, a, b);

        if (left != null && right != null)
            return root;

        return left != null ? left : right;
    }

    // LCA of three nodes
    public static BinaryTreeNode<Integer> lcaOfThreeNodes(
            BinaryTreeNode<Integer> root, int node1, int node2, int node3) {

        BinaryTreeNode<Integer> firstLCA = lca(root, node1, node2);
        return lca(root, firstLCA.data, node3);
    }
}
```


