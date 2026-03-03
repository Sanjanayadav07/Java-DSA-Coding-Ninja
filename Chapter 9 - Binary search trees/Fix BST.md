# 🌳 Recover Binary Search Tree 

This program fixes a **Binary Search Tree (BST)**  
in which exactly **two nodes are swapped by mistake**.

---

## 📌 Problem Statement

Given:
- A BST where two nodes are swapped

Restore:
- The BST property
- Without changing the tree structure
- Only swap node values

---

## 🧠 Key Insight

👉 Inorder traversal of BST should be **sorted**

If two nodes are swapped:
- There will be **1 or 2 violations** in inorder sequence
---
## 🚀 Approach
- During inorder traversal maintain:
  - prev → previous node
  - first → first wrong node
  - middle → node after first violation
  - last → second wrong node

---
## Case 1️⃣ Non-Adjacent Swap
- Two violations found
- → Swap first and last

## Case 2️⃣ Adjacent Swap
- Only one violation found
- → Swap first and middle

---
## ⏱️ Complexity:
- Time Complexity : O(n)
- Space Complexity : O(h)
---
## 💻  Code
```
public class Solution {

    static BinaryTreeNode first, middle, last, prev;

    // Inorder traversal
    private static void inorder(BinaryTreeNode root) {
        if (root == null) return;

        inorder(root.left);

        // Violation detected
        if (prev != null && root.data < prev.data) {

            // First violation
            if (first == null) {
                first = prev;
                middle = root;
            }
            // Second violation
            else {
                last = root;
            }
        }

        prev = root;
        inorder(root.right);
    }

    public static BinaryTreeNode fixBST(BinaryTreeNode root) {

        first = middle = last = null;
        prev = null;

        inorder(root);

        // Case 1: Non-adjacent nodes swapped
        if (first != null && last != null) {
            int temp = first.data;
            first.data = last.data;
            last.data = temp;
        }
        // Case 2: Adjacent nodes swapped
        else if (first != null && middle != null) {
            int temp = first.data;
            first.data = middle.data;
            middle.data = temp;
        }

        return root;
    }
}
```
