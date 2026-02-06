# 🌳 Construct Binary Tree from Inorder & Preorder Traversal 

## 📌 Problem Statement
Given two arrays:
- **Inorder Traversal**
- **Preorder Traversal**

Construct and return the **Binary Tree**.

---

## 🧠 Key Observations
- **Preorder** → Root is always visited **first**
- **Inorder** → Left subtree | Root | Right subtree
- Using preorder, we pick root
- Using inorder, we split left & right subtrees
- Recursively build the tree

---

## 🛠️ Approach
1. Maintain a global index `idx` for preorder traversal
2. Pick `preorder[idx]` as root
3. Find root position in inorder array
4. Recursively build:
   - Left subtree from left part of inorder
   - Right subtree from right part of inorder

---
## Time Complexity (TC):
   - Worst Case: O(N²)
   - Best/Average Case (with HashMap optimization): O(N)

## Space Complexity (SC): O(N)
  - Recursion stack + tree nodes.
---
## 💻 Code

```java
public class Solution {

    private static int idx;

    private static TreeNode solve(int[] preorder, int[] inorder, int start, int end) {
        if (start > end) {
            return null;
        }

        // Create root from preorder
        TreeNode root = new TreeNode(preorder[idx]);

        // Find root index in inorder
        int i;
        for (i = start; i <= end; i++) {
            if (inorder[i] == root.data) {
                break;
            }
        }

        idx++;

        // Build left and right subtrees
        root.left = solve(preorder, inorder, start, i - 1);
        root.right = solve(preorder, inorder, i + 1, end);

        return root;
    }

    public static TreeNode buildBinaryTree(int[] inorder, int[] preorder) {
        idx = 0;
        int n = preorder.length;
        return solve(preorder, inorder, 0, n - 1);
    }
}
