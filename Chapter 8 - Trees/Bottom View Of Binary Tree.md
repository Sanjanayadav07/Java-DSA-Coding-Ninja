# 🌳 Bottom View of Binary Tree 

This problem prints the **bottom view** of a binary tree using **level-order traversal**  
and tracking **horizontal distances (hd)**.

> Bottom view = nodes visible when the tree is viewed from the bottom.

---

## 🧠 Approach Used
- 🔁 **Level-order traversal (BFS)** using a queue
- 📌 Track **horizontal distance (hd)** of each node
- ✅ Use a **TreeMap** to store the **latest node at each hd**
- 🌐 Iterate the TreeMap to get nodes from **leftmost hd to rightmost hd**

---
## ⏱️ Complexity
  - Time Complexity: O(N log N)  
    - N = number of nodes (log N for TreeMap insertions)
  -  Space Complexity: O(N)  
    - Queue + TreeMap storage

---

## 💻 Code

```java
import java.util.*;

// Pair class to store node and horizontal distance
class Pair {
    TreeNode node;
    int hd;

    Pair(TreeNode node, int hd) {
        this.node = node;
        this.hd = hd;
    }
}

public class Solution {
    public static List<Integer> bottomView(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        if (root == null) return ans;

        Map<Integer, Integer> map = new TreeMap<>();
        Queue<Pair> q = new LinkedList<>();

        q.add(new Pair(root, 0));

        while (!q.isEmpty()) {
            Pair p = q.poll();
            TreeNode node = p.node;
            int hd = p.hd;

            // Overwrite value at hd → ensures bottom-most node
            map.put(hd, node.val);

            if (node.left != null)
                q.add(new Pair(node.left, hd - 1));

            if (node.right != null)
                q.add(new Pair(node.right, hd + 1));
        }

        for (int val : map.values()) {
            ans.add(val);
        }

        return ans;
    }
}
