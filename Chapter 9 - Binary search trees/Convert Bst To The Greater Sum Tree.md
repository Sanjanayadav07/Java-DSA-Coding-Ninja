# 🌳 Convert BST to Greater Sum Tree

This program converts a **Binary Search Tree (BST)** into a **Greater Sum Tree**.

In the new tree:
- Each node contains the **sum of all nodes greater than itself**.

---

## 📌 Problem Statement

Given a BST, modify it so that:
**node value = sum of all greater nodes**

---

## 🧠 Key Idea

Normal BST inorder gives **sorted order (ascending)**
**Left → Root → Right**
But we need **greater elements first**, so we use
**Right → Root → Left**

This is called **Reverse Inorder Traversal**

---

## 🚀 Algorithm

1️⃣ Traverse **right subtree** first (greater values)  
2️⃣ Store current node value  
3️⃣ Replace node value with accumulated sum  
4️⃣ Add original value to sum  
5️⃣ Traverse left subtree  

---
## ⏱️ Time Complexity
- Time Complexity : O(n)
- Space Complexity : O(h)
---

## 💻 Code

```java
class Solution {

    public static void solve(TreeNode<Integer> root, int[] sum) {
        if (root == null) return;

        // Visit right subtree (greater elements first)
        solve(root.right, sum);

        // Store original value
        int original = root.val;

        // Replace node value with sum of greater nodes
        root.val = sum[0];

        // Add original value to running sum
        sum[0] += original;

        // Visit left subtree
        solve(root.left, sum);
    }

    public static TreeNode<Integer> convertBstToGreaterSum(TreeNode<Integer> root) {
        int[] sum = new int[1]; // acts like global variable
        solve(root, sum);
        return root;
    }
}
