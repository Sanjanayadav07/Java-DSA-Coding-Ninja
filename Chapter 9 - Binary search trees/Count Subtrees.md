# 🌳 Count Subtrees with Nodes in Given Range

## 📌 Problem
Given a **Binary Tree** and a range `[low, high]`, count the number of **subtrees** where **all nodes lie within the given range**.

A subtree is valid if:
**low ≤ node.data ≤ high**
for **every node in that subtree**.

---

## 🧠 Approach

We use **Postorder Traversal (Left → Right → Root)**.

### Steps

1️⃣ Traverse the **left subtree**  
2️⃣ Traverse the **right subtree**

3️⃣ Check current node:
- If:
**root.data >= low && root.data <= high**
  AND both left and right subtrees are valid →  
This subtree is valid.

4️⃣ Increase the **count**.

---
## ⏱️  Complexity
-  Time Complexity : O(n)
-  Space Complexity : O(h)
  
---

## 💻  Code

```java
public class Solution {

    public static boolean solve(BinaryTreeNode<Integer> root, int low, int high, int[] count) {

        if (root == null) return true;

        boolean left = solve(root.left, low, high, count);
        boolean right = solve(root.right, low, high, count);

        // Check if current subtree is valid
        if (root.data >= low && root.data <= high && left && right) {
            count[0]++;      // Valid subtree root
            return true;
        }

        return false;
    }

    public static int getCount(BinaryTreeNode<Integer> root, int low, int high) {

        int[] count = new int[1];

        solve(root, low, high, count);

        return count[0];
    }
}
