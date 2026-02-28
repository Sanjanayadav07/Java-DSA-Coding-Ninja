# 🌳 Convert BST to Balanced BST

This problem converts a given **Binary Search Tree (BST)**  
into a **Balanced BST**.

---

## 🧠 Approach Used
- 📥 Perform Inorder Traversal of BST → gives sorted elements.
- 📋 Store all elements in an ArrayList.
- 🎯 Pick the middle element as root.
- 🔁 Recursively build left subtree from left half.
- 🔁 Recursively build right subtree from right half.
- 🌳 This ensures the tree is height-balanced.

---
## ⏱️ Complexity 
- Time Complexity : O(n)
- Space Complexity : O(n)

---

## 💻 Code

```java
import java.util.ArrayList;

public class Solution 
{
    static ArrayList<Integer> inorder = new ArrayList<>();

    public static TreeNode<Integer> balancedBst(TreeNode<Integer> root)
    {
        inorder.clear();          // Clear old values
        storeInorder(root);       // Store BST elements in sorted order
        return buildBalanced(0, inorder.size() - 1);  // Build balanced BST
    }

    // 📥 Store inorder traversal (sorted order)
    private static void storeInorder(TreeNode<Integer> root) {
        if (root == null) return;

        storeInorder(root.left);
        inorder.add(root.data);
        storeInorder(root.right);
    }

    // 🏗️ Build Balanced BST from sorted list
    private static TreeNode<Integer> buildBalanced(int start, int end) {
        if (start > end) return null;

        int mid = (start + end) / 2;

        TreeNode<Integer> node = new TreeNode<>(inorder.get(mid));

        node.left = buildBalanced(start, mid - 1);
        node.right = buildBalanced(mid + 1, end);

        return node;
    }
}
