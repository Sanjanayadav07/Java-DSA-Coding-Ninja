# 🌳 Maximum Leaf-to-Leaf Path Sum in Binary Tree
## 📌 Problem Statement
 - Given the root of a binary tree.
 - Find the maximum sum path between two leaf nodes.
 - The path must start and end at leaf nodes.
 - If no valid leaf-to-leaf path exists, return -1.

---
## 🧠 Approach
 - Use DFS (recursion).
 - For every node:
    - Recursively compute maximum root-to-leaf sum from left and right.
 - If both children exist:
   -  Update global maxSum:
     - left + right + root.data
- Return the larger branch sum + root value.
- If only one child exists:
  - Return that branch sum + root value.
- After traversal:
  - If no leaf-to-leaf path was found, return -1.

---
## ⏱️ Complexity Analysis
  - Time Complexity: O(N)
  - Space Complexity: O(N) (Recursion stack)
---
## 💻 Code
```
public class Solution {

    private static long maxSum;

    private static long solve(TreeNode root) {
        if (root == null) return 0;

        // Leaf node
        if (root.left == null && root.right == null) {
            return root.data;
        }

        long left = solve(root.left);
        long right = solve(root.right);

        // If both children exist → valid leaf-to-leaf path
        if (root.left != null && root.right != null) {
            maxSum = Math.max(maxSum, left + right + root.data);
            return Math.max(left, right) + root.data;
        }

        // If only one child exists
        return (root.left != null)
                ? left + root.data
                : right + root.data;
    }

    public static long findMaxSumPath(TreeNode root) {
        maxSum = Long.MIN_VALUE;

        solve(root);

        // If no valid leaf-to-leaf path found
        if (maxSum == Long.MIN_VALUE) {
            return -1;
        }

        return maxSum;
    }
}
```

