# 🌳 Kth Smallest Element in BST

## 📌 Problem
Given a **Binary Search Tree (BST)** and an integer `k`, return the **kth smallest element** in the BST.

👉 Important Property:

Inorder Traversal of BST → Sorted Order


Example:

BST → Inorder → 1 2 3 4 5 6


If `k = 3` → Answer = `3`

---

## 🧠 Approach

### Step 1: Use Inorder Traversal
Inorder traversal visits nodes in **ascending order** in a BST.

Traversal order:

Left → Root → Right


---

### Step 2: Count Nodes During Traversal

Maintain a counter while traversing:


count++


When:


count == k


Return that node because it is the **kth smallest element**.

---

### Step 3: Use Array for Counter

We use:

int[] count = {0};


Reason:
- Java passes **primitive values by value**
- Array allows the value to **persist across recursive calls**

---

## 💻 Code

```java
public class Solution {

    private static TreeNode solve(int[] count, TreeNode root, int k) {

        if (root == null) return null;

        TreeNode left = solve(count, root.left, k);

        count[0]++;

        if (count[0] == k) return root;

        TreeNode right = solve(count, root.right, k);

        return (left != null) ? left : right;
    }

    public static int kthSmallest(TreeNode root, int k) {

        int[] count = {0};

        return solve(count, root, k).data;
    }
}
```
---

⏱️ Time Complexity
O(H + k)
