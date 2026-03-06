# 🌳 Lowest Common Ancestor (LCA) in Binary Tree

## 📌 Problem
Given a **Binary Tree** and two nodes `p` and `q`, find their **Lowest Common Ancestor (LCA)**.

👉 **Lowest Common Ancestor** = The lowest node in the tree that has **both nodes as descendants**.

---

## 🧠 Approach

1️⃣ **Base Case**
- If `root == null`, return `null`.

2️⃣ **Check if current node is `p` or `q`**
- If `root.data == p.data` or `root.data == q.data`
- Then the current node itself can be the **LCA**.

3️⃣ **Search in Left and Right Subtree**
- Recursively find LCA in left subtree.
- Recursively find LCA in right subtree.

4️⃣ **Determine LCA**
- If **both left and right return non-null**, current `root` is the **LCA**.
- If only **one side returns non-null**, return that node.
- If both return **null**, return `null`.

---
## ⏱️ Complexity 
-  Time Complexity : O(n)
- Space Complexity : O(h)
---

## 💻  Code

```java
public class Solution {
    public static TreeNode LCAinaBST(TreeNode root, TreeNode p, TreeNode q) {

        // Base case
        if(root == null) return null;

        // If current node matches p or q
        if(root.data == p.data || root.data == q.data) {
            return root;
        }

        // Search left and right subtree
        TreeNode left = LCAinaBST(root.left, p, q);
        TreeNode right = LCAinaBST(root.right, p, q);

        // If both sides return non-null -> current node is LCA
        if(left != null && right != null) {
            return root;
        }

        // Otherwise return the non-null side
        return left != null ? left : right;
    }
}
