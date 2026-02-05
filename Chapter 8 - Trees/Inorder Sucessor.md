# 🌳 Inorder Successor in Binary Tree 

## 📌 Problem Statement
Given the root of a **Binary Tree** and a given node, find the **inorder successor** of that node.

👉 Inorder Successor = the node that appears **immediately after** the given node in **inorder traversal**.

---

## 🧠 Approach
- Perform **Inorder Traversal (Left → Root → Right)**
- Keep a boolean flag `found` to track when the given node is encountered
- The **very next node visited after `node`** is the inorder successor
- Stop traversal once successor is found

---
## ⏱️ Complexity
  - Time Complexity: O(N)
  - Space Complexity: O(H)
      - (H = height of tree due to recursion stack)

---

## 💻 Java Code

```java
public class Solution {

    static BinaryTreeNode<Integer> successor = null;
    static boolean found = false;

    public static BinaryTreeNode<Integer> inorderSuccesor(
            BinaryTreeNode<Integer> root,
            BinaryTreeNode<Integer> node) {

        successor = null;
        found = false;
        inorder(root, node);
        return successor;
    }

    private static void inorder(BinaryTreeNode<Integer> root,
                                BinaryTreeNode<Integer> node) {

        if (root == null || successor != null) {
            return;
        }

        inorder(root.left, node);

        if (found && successor == null) {
            successor = root;
            return;
        }

        if (root == node) {
            found = true;
        }

        inorder(root.right, node);
    }
}
