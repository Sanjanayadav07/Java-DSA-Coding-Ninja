# 🌳 Convert Binary Tree to Binary Search Tree 

This program converts a **Binary Tree** into a **Binary Search Tree (BST)**  
without changing the tree structure.

---

## 📌 Problem Statement

Given:
- A Binary Tree (not necessarily BST)

Convert it into a BST such that:
- Tree structure remains same
- Only node values are rearranged

---

## 🧠 Key Idea

👉 Inorder traversal of a BST is always **sorted**.

So approach:

1️⃣ Store inorder traversal of the given tree  
2️⃣ Sort the collected values  
3️⃣ Reassign values back using inorder traversal  

Since structure stays same,  
and inorder is sorted → Tree becomes BST ✅

---

## 🚀 Approach

### Step 1: Collect Inorder Values
``` id="step1"
Left → Root → Right
```
### Step 2: Sort Values
- Collections.sort(list)
  
### Step 3: Fill Tree Again (Inorder)
 - Replace node values one by one from sorted list.
---
## ⏱️ Complexity Analysis
- Time	O(n log n)
- Space	O(n)

---

## 🧑‍💻  Code
```
public class Solution {

    // Step 1: Store inorder traversal
    public static void inorderTree(BinaryTreeNode<Integer> root,
                                   ArrayList<Integer> ans) {

        if (root == null) return;

        inorderTree(root.left, ans);
        ans.add(root.data);
        inorderTree(root.right, ans);
    }

    // Step 3: Put sorted values back using inorder
    public static void inorderBST(BinaryTreeNode<Integer> root,
                                  ArrayList<Integer> ans,
                                  int[] idx) {

        if (root == null) return;

        inorderBST(root.left, ans, idx);

        root.data = ans.get(idx[0]);
        idx[0]++;

        inorderBST(root.right, ans, idx);
    }

    public static BinaryTreeNode<Integer> binaryTreeToBst(
            BinaryTreeNode<Integer> root) {

        if (root == null) return null;

        ArrayList<Integer> ans = new ArrayList<>();

        // Collect values
        inorderTree(root, ans);

        // Sort values
        Collections.sort(ans);

        // Refill tree
        int[] idx = new int[]{0};
        inorderBST(root, ans, idx);

        return root;
    }
}
