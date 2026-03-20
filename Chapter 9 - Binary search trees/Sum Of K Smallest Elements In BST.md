## 📌 Problem
Given a **Binary Search Tree (BST)** and an integer `k`, find the **sum of the k smallest elements**.

---

## 🧠 Key Idea
- BST property:
- Inorder Traversal → Sorted Order (Ascending)
- So the **first k elements in inorder traversal** are the **k smallest elements**.

---

## 🛠️ Approach

### Step 1: Perform Inorder Traversal
- Traverse the BST in:
- Left → Root → Right
---

### Step 2: Keep Track of Count

- Use an array `k[]` to track remaining elements
- Add node values to sum until `k == 0`

---

### Step 3: Stop Early (Optimization)
- if k <= 0 → stop traversal
- This avoids unnecessary traversal.
---

## 💻 Code

```java
class Solution {

    private static void solve(BinaryTreeNode<Integer> root, int[] k, long[] sum) {

        if (root == null || k[0] <= 0) return;

        // Left subtree
        solve(root.left, k, sum);

        // Process current node
        if (k[0] > 0) {
            sum[0] += root.data;
            k[0]--;
        }

        // Right subtree
        solve(root.right, k, sum);
    }

    public static long ksmallestElementSum(BinaryTreeNode<Integer> root, int k) {

        long[] sum = new long[1];
        int[] kk = new int[]{k};

        solve(root, kk, sum);

        return sum[0];
    }
}
```
### ⏱️ Time Complexity
- O(H + K)
- Where:
  - H = height of tree
- We traverse only until k elements are processed
- Worst case: O(N)
### 📦 Space Complexity
- O(H)
