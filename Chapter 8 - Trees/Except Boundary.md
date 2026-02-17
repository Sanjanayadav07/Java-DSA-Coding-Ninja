# 🌳 Sum of Nodes Except Boundary Nodes 

This program calculates the **sum of all non-boundary nodes** in a Binary Tree.

---

## 📌 Problem Statement

Given a Binary Tree, return the sum of all nodes **excluding boundary nodes**.

### Boundary Nodes Include:
1. Root node
2. Left boundary (excluding leaves)
3. Right boundary (excluding leaves)
4. All leaf nodes

Final Answer:
**Total Sum - Boundary Sum**

---

## 🧠 Approach

### Step 1️⃣: Find Total Sum
Use recursion to calculate sum of all nodes.

### Step 2️⃣: Calculate Boundary Sum
Boundary consists of:
- Root
- Left boundary (excluding leaf)
- All leaf nodes
- Right boundary (excluding leaf)

### Step 3️⃣: Subtract Boundary Sum from Total Sum

If result becomes negative, return `0`.

---
## ⏱️ Complexity Analysis
 - Time Complexity: O(n)
 - Space Complexity: O(h) (recursion stack)

---

## 🧑‍💻 Code

```java
public class Solution {

    public static int inorder(BinaryTreeNode<Integer> root) {
        if (root == null) return 0;
        return root.data + inorder(root.left) + inorder(root.right);
    }

    // Check if node is a leaf
    public static boolean isLeaf(BinaryTreeNode<Integer> root) {
        return root != null && root.left == null && root.right == null;
    }

    // Left boundary sum
    public static void leftSum(BinaryTreeNode<Integer> root, int[] ans) {
        if (root == null || isLeaf(root)) return;

        ans[0] += root.data;

        if (root.left != null) {
            leftSum(root.left, ans);
        } else {
            leftSum(root.right, ans);
        }
    }

    // Right boundary sum
    public static void rightSum(BinaryTreeNode<Integer> root, int[] ans) {
        if (root == null || isLeaf(root)) return;

        ans[0] += root.data;

        if (root.right != null) {
            rightSum(root.right, ans);
        } else {
            rightSum(root.left, ans);
        }
    }

    // Sum of all leaf nodes
    public static void leafSum(BinaryTreeNode<Integer> root, int[] ans) {
        if (root == null) return;

        leafSum(root.left, ans);

        if (isLeaf(root)) {
            ans[0] += root.data;
        }

        leafSum(root.right, ans);
    }

    // Main function
    public static int exceptBoundary(BinaryTreeNode<Integer> root) {

        if (root == null) return 0;

        int totalSum = inorder(root);

        int[] ans = new int[1];

        // Add root
        ans[0] += root.data;

        // Add left boundary
        leftSum(root.left, ans);

        // Add leaf nodes
        leafSum(root, ans);

        // Add right boundary
        rightSum(root.right, ans);

        int result = totalSum - ans[0];

        return Math.max(result, 0);
    }
}
