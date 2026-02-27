# 🌳 Convert BST to Min Heap (Without Changing Structure)

This program converts a **Binary Search Tree (BST)** into a **Min Heap**  
while keeping the **same tree structure**.

---

## 📌 Problem Statement

Given:
✔ A Binary Search Tree

Convert it into:
✔ A Min Heap

Conditions:
- Tree structure should remain same
- Only node values can change

---

## 🧠 Key Observation

### BST Property:
👉 Inorder traversal = Sorted order

### Min Heap Property:
👉 Parent ≤ Children

So idea is simple:

1. Store BST inorder → gives sorted values
2. Fill tree in preorder using sorted values

Because preorder ensures:
✔ Parent is filled before children  
✔ Smaller values go to top  

Result → Min Heap 🎯

---

## 🚀 Approach

### Step 1: Store Inorder Traversal

```java
Left → Root → Right
This gives sorted values.
```
### Step 2: Fill using Preorder
**Root → Left → Right**
- Assign values sequentially from sorted array.

- This ensures:

- Parent gets smaller value
- Children get larger values

- → Min Heap satisfied ✅
---

## 🧑‍💻  Code
public class Solution {

    static int index;

    // Step 1: Store inorder (sorted values)
    public static void getInorder(BinaryTreeNode root, ArrayList<Integer> ans) {
        if (root == null) return;

        getInorder(root.left, ans);
        ans.add(root.data);
        getInorder(root.right, ans);
    }

    // Step 2: Fill using preorder
    public static void getPreorder(BinaryTreeNode root, ArrayList<Integer> ans) {
        if (root == null) return;

        root.data = ans.get(index++);
        getPreorder(root.left, ans);
        getPreorder(root.right, ans);
    }

    // Main Function
    public static BinaryTreeNode convertBST(BinaryTreeNode root) {
        ArrayList<Integer> ans = new ArrayList<>();

        getInorder(root, ans);   // Step 1
        index = 0;
        getPreorder(root, ans);  // Step 2

        return root;
    }
