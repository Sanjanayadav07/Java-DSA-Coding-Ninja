# 🌳 Left View of Binary Tree

## 📌 Problem Statement

  - Given the root of a binary tree, print its **Left View**
  - The **Left View** contains all nodes that are first nodes at their level when the tree is seen from the left side.

---

## 🧠 Approach
- Use **Level Order Traversal (BFS)**  with a queue.
- For each level:
    - Print or store the first node.
    - Enqueue its left and right children.
    - Continue until the queue is empty.
---
## ⏱️ Complexity Analysis
  -  Time Complexity: O(N)
  → Each node is visited exactly once using level order traversal.

  - Space Complexity: O(N)
  → Queue can store up to N nodes in the worst case (last level of the tree).
---
## 💻  Code
```
import java.util.*;

public class Solution {

    public static void printLeftView(TreeNode<Integer> root) {
        if (root == null) return;

        Queue<TreeNode<Integer>> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) {
            int n = q.size();

            // Print leftmost node of current level
            System.out.print(q.peek().data + " ");

            while (n-- > 0) {
                TreeNode<Integer> temp = q.poll();

                if (temp.left != null)
                    q.add(temp.left);

                if (temp.right != null)
                    q.add(temp.right);
            }
        }
    }
}
```
---
