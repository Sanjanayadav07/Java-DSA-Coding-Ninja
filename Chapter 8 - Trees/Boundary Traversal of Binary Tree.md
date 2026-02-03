# 🌳 Boundary Traversal of Binary Tree 

## 📌 Problem Statement
Given the root of a binary tree, print the **boundary traversal** of the tree in **anti-clockwise order**.

Boundary traversal includes:
1. Root node  
2. Left boundary (excluding leaf nodes)  
3. All leaf nodes (left to right)  
4. Right boundary (excluding leaf nodes, bottom to top)

---

## 🧠 Approach
- Add the **root** node first
- Traverse the **left boundary** (excluding leaves)
- Traverse **all leaf nodes**
- Traverse the **right boundary** in reverse order
- Use recursion for clean and efficient traversal

---
## ⏱️ Complexity Analysis
  - Time Complexity: O(N)
  - Space Complexity: O(N)
---

## 💻 Code

```java
import java.util.*;

public class Solution {

    // Left boundary (excluding leaf nodes)
    private static void leftBoundary(TreeNode root, ArrayList<Integer> ans) {
        if (root == null) return;

        if (root.left != null) {
            ans.add(root.data);
            leftBoundary(root.left, ans);
        } else if (root.right != null) {
            ans.add(root.data);
            leftBoundary(root.right, ans);
        }
    }

    // Leaf nodes
    private static void leafNodes(TreeNode root, ArrayList<Integer> ans) {
        if (root == null) return;

        leafNodes(root.left, ans);

        if (root.left == null && root.right == null) {
            ans.add(root.data);
        }

        leafNodes(root.right, ans);
    }

    // Right boundary (excluding leaf nodes, reversed)
    private static void rightBoundary(TreeNode root, ArrayList<Integer> ans) {
        if (root == null) return;

        if (root.right != null) {
            rightBoundary(root.right, ans);
            ans.add(root.data);
        } else if (root.left != null) {
            rightBoundary(root.left, ans);
            ans.add(root.data);
        }
    }

    public static ArrayList<Integer> traverseBoundary(TreeNode root) {
        ArrayList<Integer> ans = new ArrayList<>();
        if (root == null) return ans;

        ans.add(root.data);           // Root
        leftBoundary(root.left, ans);
        leafNodes(root.left, ans);
        leafNodes(root.right, ans);
        rightBoundary(root.right, ans);

        return ans;
    }
}
