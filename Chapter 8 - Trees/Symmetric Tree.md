# 🌳 Check if Binary Tree is Symmetric 

This program checks whether a Binary Tree is **Symmetric (Mirror of itself)**.

---

## 📌 Problem Statement

A Binary Tree is **symmetric** if:

- Left subtree is a mirror reflection of the right subtree.

---

## 🧠 Approach

We use **Recursion** to compare the left and right subtrees.

### Base Cases:

1️⃣ If root is `null` → Tree is symmetric  
2️⃣ If both nodes are `null` → Return `true`  
3️⃣ If one is `null` → Return `false`  

### Recursive Check:

For symmetry:
- Left node value == Right node value  
- Left's left subtree == Right's right subtree  
- Left's right subtree == Right's left subtree  

---

## 🧑‍💻 Code

```java
public class Solution {

    public static boolean isSymmetric(BinaryTreeNode<Integer> root) {

        if (root == null) return true;

        return check(root.left, root.right);
    }

    private static boolean check(BinaryTreeNode<Integer> l,
                                 BinaryTreeNode<Integer> r) {

        // Both null
        if (l == null && r == null) return true;

        // One null
        if (l == null || r == null) return false;

        // Same value + mirror structure
        return l.data.equals(r.data)
                && check(l.left, r.right)
                && check(l.right, r.left);
    }
}
