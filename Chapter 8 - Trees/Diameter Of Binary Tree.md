# Diameter of Binary Tree 🌳

This project contains a Java implementation to calculate the **diameter of a binary tree**.

---

## 📌 Problem Statement

Given a binary tree, find its **diameter**.

👉 The diameter of a binary tree is the **number of edges in the longest path between any two nodes** in the tree.

The path may or may not pass through the root.

---

## 💡 Approach

We use a **single DFS traversal** to compute:

- Height of left subtree
- Height of right subtree
- Update maximum diameter at every node

### Key Idea:

For every node:
```
Diameter through node = height(left) + height(right)

```

We maintain a global maximum and update it during recursion.

---
## 🧠 Complexity Analysis
- Time Complexity: O(N)
  - (Each node is visited exactly once)
- Space Complexity: O(H)
   - (Recursion stack, where H = height of tree)

---

## 🚀 Code

```java
public class Solution {

    public static int diameterOfBinaryTree(TreeNode<Integer> root) {
        if (root == null) return 0;

        int[] result = {0};   // stores maximum diameter
        diameter(root, result);
        return result[0];
    }

    private static int diameter(TreeNode<Integer> root, int[] result) {
        if (root == null) return 0;

        int left = diameter(root.left, result);
        int right = diameter(root.right, result);

        // diameter passing through this node
        result[0] = Math.max(result[0], left + right);

        // return height
        return Math.max(left, right) + 1;
    }
}

