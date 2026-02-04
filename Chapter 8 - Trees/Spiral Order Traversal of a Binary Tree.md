# 🌪️ Spiral (Zigzag) Order Traversal of Binary Tree 

## 📌 Problem Statement
Given the root of a binary tree, return its **spiral (zigzag) order traversal**.

Spiral order means:
- First level → **Left to Right**
- Second level → **Right to Left**
- Third level → **Left to Right**
- … and so on.

---

## 🧠 Approach
- Use **Level Order Traversal (BFS)** with a **Queue**
- Maintain a boolean flag `leftToRight` to control direction
- For each level:
  - Store values in an array
  - Place values at correct index based on direction
- Append the level array to the final answer
- Toggle direction after every level

---
## ⏱️ Complexity Analysis
  - Time Complexity: O(N)
  - Space Complexity: O(N)
---
## 💻 Code

```java
import java.util.*;

public class Solution {
    public static ArrayList<Integer> spiralOrder(BinaryTreeNode<Integer> root) {

        ArrayList<Integer> ans = new ArrayList<>();
        if (root == null) return ans;

        Queue<BinaryTreeNode<Integer>> q = new LinkedList<>();
        q.add(root);

        boolean leftToRight = true;

        while (!q.isEmpty()) {

            int size = q.size();
            int[] level = new int[size];

            for (int i = 0; i < size; i++) {
                BinaryTreeNode<Integer> node = q.poll();

                int index;
                if (leftToRight) {
                    index = i;              // Left → Right
                } else {
                    index = size - 1 - i;   // Right → Left
                }

                level[index] = node.data;

                if (node.left != null) q.add(node.left);
                if (node.right != null) q.add(node.right);
            }

            // Add current level to answer
            for (int val : level) {
                ans.add(val);
            }

            leftToRight = !leftToRight; // change direction
        }

        return ans;
    }
}
