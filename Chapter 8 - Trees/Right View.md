# 🌳 Right View of Binary Tree (Level Order)

This problem prints the **right view** of a binary tree using **level-order traversal**.

> Right view = nodes visible when the tree is viewed from the right side.

---

## 🧠 Approach Used
- 🔁 **Level-order traversal (BFS)** using a queue
- ✅ For each level, **add the last node** to the answer
- 👀 This ensures the **rightmost node at each level** is captured
- 🔄 Add children of current node to the queue for the next level.
- 🎯 Repeat until all levels are processed.

---
## ⏱️ Complexity :
  - Time Complexity: O(N)
  - Space Complexity: O(W)
     -  W = maximum width of the tree
---

## 💻 Code

```java
import java.util.*;

public class Solution {
    public static ArrayList<Integer> printRightView(BinaryTreeNode<Integer> root) {
        ArrayList<Integer> ans = new ArrayList<>();
        if (root == null) return ans;

        Queue<BinaryTreeNode<Integer>> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) {
            int n = q.size();

            for (int i = 0; i < n; i++) {
                BinaryTreeNode<Integer> temp = q.poll();

                // last node of this level = Right View
                if (i == n - 1) {
                    ans.add(temp.data);
                }

                if (temp.left != null)
                    q.add(temp.left);

                if (temp.right != null)
                    q.add(temp.right);
            }
        }
        return ans;
    }
}
