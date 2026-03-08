# 🌳 Pair Sum in BST

## 📌 Problem
Given a **Binary Search Tree (BST)** and an integer `k`, determine if there exist **two nodes** in the BST such that their **sum equals `k`**.

Return:
- `true` → if such a pair exists  
- `false` → otherwise

---

## 🧠 Approach

### Step 1: Convert BST to Sorted Array
- Perform **Inorder Traversal** of BST.
- Inorder traversal of BST gives **sorted order**.

### Step 2: Apply Two Pointer Technique

Use two pointers:

**left → start of list**
**right → end of list**

Then:

- If `sum == k` → pair found ✅  
- If `sum < k` → move `left++`  
- If `sum > k` → move `right--`

---
## ⏱️ Complexity
-  Time Complexity : O(n)
-  Space  Complexity : O(n)
---

## 💻 Code

```java
import java.util.ArrayList;

public class Solution {

    public static void inorderTraversal(TreeNode root, ArrayList<Integer> inorder) {
        if (root == null) return;

        inorderTraversal(root.left, inorder);
        inorder.add(root.data);
        inorderTraversal(root.right, inorder);
    }

    public static boolean pairSumBst(TreeNode root, int k) {

        ArrayList<Integer> inorder = new ArrayList<>();

        // Convert BST to sorted array
        inorderTraversal(root, inorder);

        int left = 0;
        int right = inorder.size() - 1;

        // Two pointer approach
        while (left < right) {

            int currentSum = inorder.get(left) + inorder.get(right);

            if (currentSum == k) {
                return true;
            }

            if (currentSum < k) {
                left++;
            } else {
                right--;
            }
        }

        return false;
    }
}
