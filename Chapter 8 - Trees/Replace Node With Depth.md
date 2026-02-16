# 🌳 Change Binary Tree to Depth Tree 

This program modifies a Binary Tree such that:

- Each node’s value is replaced with its **depth level**
- Root depth = `0`
- For every child, depth = `parent depth + 1`

---
## ⏱️ Complexity Analysis
 - Time Complexity: O(n)
 - Space Complexity: O(h)
    - (h = height of tree, recursion stack)

---

## 🧠 Approach

We use **Preorder Traversal (Root → Left → Right)**.

### Steps:
1. Start from root with depth = `0`
2. Replace node value with current depth
3. Recursively call for:
   - Left child with `depth + 1`
   - Right child with `depth + 1`

Since we update before recursion, preorder traversal is ideal.

---

## 🧑‍💻 Code

```java
public class Solution {

    public static BinaryTreeNode<Integer> changeToDepthTree(BinaryTreeNode<Integer> root) {
        changeToDepthTreeAns(root, 0);
        return root;
    }

    public static void changeToDepthTreeAns(BinaryTreeNode<Integer> root, int pos) {
        if (root == null) return;

        root.data = pos;

        changeToDepthTreeAns(root.left, pos + 1);
        changeToDepthTreeAns(root.right, pos + 1);
    }
}
