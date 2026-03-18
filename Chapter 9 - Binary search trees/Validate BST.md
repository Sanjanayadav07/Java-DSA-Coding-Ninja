# 🌳 Validate Binary Search Tree (BST)

## 📌 Problem
Given a **Binary Tree**, check whether it is a **valid Binary Search Tree (BST)**.

Return:
- `true` → if valid BST  
- `false` → otherwise  

---

## 🧠 Key Idea

In a valid BST:


Left subtree → values < root
Right subtree → values > root


But this must hold **for every node with a valid range**, not just direct children.

---

## 🛠️ Approach 

We pass a **valid range (min, max)** for each node:

### Step 1: Start with full range


(-∞, +∞)


---

### Step 2: Validate Current Node


if node.data <= min OR node.data >= max → invalid


---

### Step 3: Recursively Check Subtrees

- Left subtree:

(min, root.data)


- Right subtree:

(root.data, max)


---

## 💻 Code

```java
public class Solution {

    public static boolean validateBST(BinaryTreeNode<Integer> root) {
        return isValid(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private static boolean isValid(BinaryTreeNode<Integer> root, long min, long max) {

        if (root == null) return true;

        if (root.data <= min || root.data >= max) {
            return false;
        }

        return isValid(root.left, min, root.data) &&
               isValid(root.right, root.data, max);
    }
}
```
---
### ⏱️ Time Complexity
- O(N)
- Every node is visited once.

### 📦 Space Complexity
- O(H)
- Where:
  - H = height of tree
- Balanced Tree → O(log N)
- Skewed Tree → O(N)
