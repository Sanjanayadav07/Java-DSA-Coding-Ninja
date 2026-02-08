# 🌳 Top View of Binary Tree 

## 📌 Problem Statement
Given the root of a binary tree, return the **Top View** of the binary tree.  
The **Top View** contains the nodes that are visible when the tree is viewed from the top.

---

## 🧠 Approach
- Use **Level Order Traversal (BFS)**  
- Track **Horizontal Distance (HD)** for each node:
  - Root → HD = 0
  - Left child → HD - 1
  - Right child → HD + 1
- Use a **TreeMap** to store the **first node encountered** at each horizontal distance
- TreeMap keeps keys sorted → ensures left-to-right order in output

---
## ⏱️ Complexity Analysis
   - Time Complexity: O(N log N)
       - (TreeMap insertion for each node)
   - Space Complexity: O(N)
       - (Queue + Map)
---

## 💻 Code 

```java
import java.util.*;

class TreeNodeWithHorizontalDistance {

    TreeNode node;
    int horizontalDistance;

    TreeNodeWithHorizontalDistance(TreeNode node, int horizontalDistance) {
        this.node = node;
        this.horizontalDistance = horizontalDistance;
    }
}

public class Solution {

    public static List<Integer> getTopView(TreeNode root) {

        if (root == null) return new ArrayList<>();

        List<Integer> topViewNodes = new ArrayList<>();

        // HD -> Node value (first occurrence only)
        Map<Integer, Integer> topViewMap = new TreeMap<>();

        Queue<TreeNodeWithHorizontalDistance> q = new LinkedList<>();
        q.add(new TreeNodeWithHorizontalDistance(root, 0));

        while (!q.isEmpty()) {

            TreeNodeWithHorizontalDistance curr = q.poll();
            int hd = curr.horizontalDistance;
            TreeNode node = curr.node;

            // Store only first node at this HD
            if (!topViewMap.containsKey(hd)) {
                topViewMap.put(hd, node.data);
            }

            if (node.left != null) {
                q.add(new TreeNodeWithHorizontalDistance(node.left, hd - 1));
            }

            if (node.right != null) {
                q.add(new TreeNodeWithHorizontalDistance(node.right, hd + 1));
            }
        }

        for (int val : topViewMap.values()) {
            topViewNodes.add(val);
        }

        return topViewNodes;
    }
}
