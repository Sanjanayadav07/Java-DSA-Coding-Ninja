# 🌳 Check Special Binary Tree 

This program checks whether a Binary Tree is a **Special Binary Tree**.

---

## 📌 Problem Statement

A Binary Tree is called **Special** if:

- Every node has either:
  - **0 children** (Leaf Node)  
  OR  
  - **2 children**  

👉 No node should have exactly **1 child**.

---

## 🧠 Approach (Recursive)

### ✅ Base Case
- If tree is empty → return `true`

### ❌ Invalid Case
- If one child is null and the other is not → return `false`

### 🔁 Recursive Step
- Recursively check left subtree
- Recursively check right subtree
- Both must be special

---
## ⏱️ Complexity Analysis
 - Time	O(n)
 - Space	O(h) (recursion stack)

---

## 🧑‍💻 Code

```java
public class Solution {

    public static boolean isSpecialBinaryTree(BinaryTreeNode root) {

        // Base case: empty tree is special
        if (root == null) {
            return true;
        }

        // If one child exists and the other doesn't → Not special
        if (root.left != null && root.right == null) {
            return false;
        }

        if (root.left == null && root.right != null) {
            return false;
        }

        // Recursively check left and right subtrees
        return isSpecialBinaryTree(root.left) &&
               isSpecialBinaryTree(root.right);
    }
}
