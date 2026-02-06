# 🌳 Construct Complete Binary Tree from Array

## 📌 Problem Statement
Given an array of integers, construct a **Complete Binary Tree (CBT)**  
by inserting elements **level by level from left to right**.

---

## 🧠 Approach
- Use a **Queue** to keep track of tree nodes
- Start with the first element as the root
- For each node:
  - Assign left child
  - Assign right child
- Continue until the array is fully processed

This ensures **level order construction**, which is required for a CBT.

---
## Complexity :
  - Time Complexity  : O(N)
  - Space Complexity : O(N)

---
## 💻 Code

```java
import java.util.*;

public class Solution {

    public static TreeNode constructCBT(int[] arr) {

        // Edge case
        if (arr == null || arr.length == 0) {
            return null;
        }

        TreeNode root = new TreeNode(arr[0]);
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);

        int i = 1;

        while (i < arr.length) {
            TreeNode curr = q.poll();

            if (i < arr.length) {
                curr.left = new TreeNode(arr[i++]);
                q.add(curr.left);
            }

            if (i < arr.length) {
                curr.right = new TreeNode(arr[i++]);
                q.add(curr.right);
            }
        }

        return root;
    }
}
