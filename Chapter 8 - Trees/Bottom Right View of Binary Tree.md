# 🌳 Bottom Right View of Binary Tree
## 📌 Problem Statement

- Given the root of a binary tree, return the Bottom Right View of the tree.
- The bottom right view consists of the last visible node at each diagonal/depth, preferring the rightmost node.
---
## 🧠 Approach
- Use DFS (recursion).
- Maintain a HashMap<depth, nodeValue>.
- For every depth:
   - Overwrite the value so the last visited node (bottom/right) remains.
- Traversal rule:
  - Left child → depth + 1
  - Right child → same depth
- Collect values from the map.
- Sort the result if required.
---

## ⏱️ Complexity Analysis
 - Time Complexity: O(N)
 - Space Complexity: O(N)

---
## 💻 Code
```
import java.util.*;

public class Solution {    

    public static ArrayList<Integer> bottomRightView(BinaryTreeNode<Integer> root) {

        ArrayList<Integer> ans = new ArrayList<>();
        if (root == null) return ans;

        Map<Integer, Integer> map = new HashMap<>();
        solve(root, map, 0);

        for (int key : map.keySet()) {
            ans.add(map.get(key));
        }

        Collections.sort(ans);
        return ans;
    }

    private static void solve(BinaryTreeNode<Integer> root,
                              Map<Integer, Integer> map,
                              int depth) {

        if (root == null) return;

        // overwrite to keep bottom/rightmost node
        map.put(depth, root.data);

        solve(root.left, map, depth + 1);
        solve(root.right, map, depth);
    }
}
```
----
