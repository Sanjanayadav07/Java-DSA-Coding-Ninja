# 🌳 Count Univalue Subtrees 

This program counts the number of **Univalue Subtrees** in a Binary Tree.

A **Univalue Subtree** is a subtree where:
- All nodes have the **same value**

---

## 🧠 Approach

We use **Postorder Traversal (Left → Right → Root)**.

### Steps:
1. Recursively check left subtree
2. Recursively check right subtree
3. If:
   - Both subtrees are univalue
   - Left child (if exists) has same value as root
   - Right child (if exists) has same value as root  
   
   ➝ Then current subtree is also univalue

4. Increase count

We use an `int[]` array to maintain a **mutable counter**.

---

## ⏱️ Complexity Analysis
 - Time Complexity: O(n)
 - Space Complexity: O(h) (recursion stack, h = tree height)

---
## 🧑‍💻 Code

```java
public class Solution {

    public static int countUnivalTrees(BinaryTreeNode<Integer> root) {
        int[] count = new int[1];   // mutable counter
        isUnival(root, count);
        return count[0];
    }

    private static boolean isUnival(BinaryTreeNode<Integer> node, int[] count) {
        if (node == null) return true;

        boolean left = isUnival(node.left, count);
        boolean right = isUnival(node.right, count);

        // If any subtree is not univalue
        if (!left || !right) return false;

        if (node.left != null && !node.left.data.equals(node.data))
            return false;

        if (node.right != null && !node.right.data.equals(node.data))
            return false;

        // Current subtree is univalue
        count[0]++;
        return true;
    }
}
