# 🌳➡️🔺 Convert BST to Min Heap 

## 📌 Problem
Given a **Binary Search Tree (BST)**, convert it into a **Min Heap** such that:

- ✔ Tree structure remains **same**
- ✔ It satisfies **Min Heap property**
- Parent ≤ Children
---

## 🧠 Key Idea

- Use traversal combination:
- Inorder → Sorted values
- Preorder → Assign values (root first)


👉 Why this works?
- Inorder gives **ascending order**
- Preorder ensures **smallest value goes to root first**

---

## 🛠️ Approach

### 🔹 Step 1: Inorder Traversal
- Store BST values in sorted order
- Left → Root → Right
---

### 🔹 Step 2: Preorder Traversal
- Replace node values using sorted list
- Root → Left → Right


👉 This ensures:
- Root gets smallest value
- Children get larger values
→ Min Heap property satisfied ✅

---

## 💻 Code

```java
import java.util.*;
import java.io.*;

public class Solution {

    // Step 1: Store inorder (sorted values)
    public static void inorder(BinaryTreeNode root, ArrayList<Integer> vals) {
        if (root == null) return;

        inorder(root.left, vals);
        vals.add(root.data);
        inorder(root.right, vals);
    }

    // Step 2: Fill using preorder
    public static void preorder(BinaryTreeNode root, ArrayList<Integer> vals, int[] index) {
        if (root == null) return;

        root.data = vals.get(index[0]++);
        preorder(root.left, vals, index);
        preorder(root.right, vals, index);
    }

    public static BinaryTreeNode convertBST(BinaryTreeNode root) {

        ArrayList<Integer> vals = new ArrayList<>();

        // Get sorted values
        inorder(root, vals);

        // Replace values to form Min Heap
        preorder(root, vals, new int[]{0});

        return root;
    }
}
```
---
### ⏱️ Time Complexity
- O(N)
- Inorder traversal → O(N)
- Preorder traversal → O(N)
### 📦 Space Complexity
- O(N)
- ArrayList stores all node values
