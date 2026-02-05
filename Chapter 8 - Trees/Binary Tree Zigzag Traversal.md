# 🔀 ZigZag Traversal of Binary Tree 

## 📌 Problem Statement
Given the root of a binary tree, return its **zigzag traversal**.

Zigzag traversal means:
- Level 1 → Left to Right  
- Level 2 → Right to Left  
- Level 3 → Left to Right  
- and so on…

---

## 🧠 Approach
- Use **Breadth First Search (BFS)** with a **Queue**
- Traverse tree level by level
- Maintain a boolean flag `leftToRight`
- Store each level in an array and insert values based on direction
- Toggle direction after each level

---
## ⏱️ Complexity
  - Time Complexity: O(N)
  - Space Complexity: O(N)
---

## 💻 Code

```java
import java.util.* ;
import java.io.*; 

public class Solution {
    public static List<Integer> zigZagTraversal(BinaryTreeNode<Integer> root) {

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
                    index = i;                // Left → Right
                } else {
                    index = size - 1 - i;     // Right → Left
                }

                level[index] = node.data;

                if (node.left != null) q.add(node.left);
                if (node.right != null) q.add(node.right);
            }

            for (int val : level) {
                ans.add(val);
            }

            leftToRight = !leftToRight; // direction toggle
        }

        return ans;
    }
}
