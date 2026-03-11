# 🌳 BST Range Queries

## 📌 Problem
Given a **Binary Search Tree (BST)** and multiple queries of the form `[L, R]`, return the number of nodes in the BST whose values lie in each range.

---

## 🧠 Approach

### Step 1: Convert BST to Sorted List
- Perform **Inorder Traversal** of BST.
- Inorder traversal of BST gives **sorted values**.
**id="m7tx5z1"
BST → Inorder → Sorted List**

### Step 2: Process Each Query
- For each query [L, R]:
- Use binary search to find the first node ≥ L
- Use binary search to find the last node ≤ R

### Step 3: Count Nodes in Range
- Number of nodes in range = y - x + 1
- If binary search returns negative:
- Adjust index as x = Math.abs(x) - 1
- Adjust index as y = Math.abs(y) - 2

---

## 💻  Code
```
import java.util.ArrayList;
import java.util.Collections;

public class Solution {

    private static void inorder(BinaryTreeNode<Integer> root, ArrayList<Integer> list) {
        if(root == null) return;

        inorder(root.left, list);
        list.add(root.data);
        inorder(root.right, list);
    }

    public static ArrayList<Integer> bstQueries(BinaryTreeNode<Integer> root, int q, int[][] queries) {

        ArrayList<Integer> list = new ArrayList<>();
        ArrayList<Integer> ans = new ArrayList<>();

        // Convert BST → Sorted List
        inorder(root, list);

        for(int i = 0; i < q; i++) {
            int L = queries[i][0];
            int R = queries[i][1];

            int x = Collections.binarySearch(list, L);
            int y = Collections.binarySearch(list, R);

            if(x < 0) x = Math.abs(x) - 1;
            if(y < 0) y = Math.abs(y) - 2;

            ans.add(y - x + 1);
        }

        return ans;
    }
}
```

---
### ⏱️ Time Complexity
- O(N + Q * log N)

### 📦 Space Complexity
- O(N)
