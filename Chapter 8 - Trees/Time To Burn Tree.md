# 🔥 Burning Binary Tree 

This program calculates the **time required to burn an entire Binary Tree**
starting from a given target node.

---

## 📌 Problem Statement

Given:
- A Binary Tree
- A starting node value

Each second:
- Fire spreads to:
  - Left child
  - Right child
  - Parent

Return the **total time required** to burn the complete tree.

---

## 🧠 Approach

We solve this in **2 Steps (BFS Based)**:

### ✅ Step 1: Map Parents
Since Binary Tree nodes don’t have parent pointers,
we perform a BFS traversal to:
- Store each node’s parent in a `HashMap`
- Find the target node

---

### ✅ Step 2: Burn the Tree (Multi-directional BFS)

Start BFS from the target node.

From each node, fire spreads to:
- Left child
- Right child
- Parent

We track visited nodes to avoid revisiting.

Each BFS level = **1 second**

---
## ⏱️ Complexity Analysis
 - Operation	Complexity
    - Parent Mapping BFS	O(n)
    - Burning BFS	O(n)
- Total Time	O(n)
- Space	O(n)

---

## 🧑‍💻 Code

```java
import java.util.*;

public class Solution {

    // BFS to calculate maximum distance (time to burn)
    private static int findMaxDistance(
            Map<BinaryTreeNode<Integer>, BinaryTreeNode<Integer>> parentMap,
            BinaryTreeNode<Integer> target) {

        Queue<BinaryTreeNode<Integer>> queue = new LinkedList<>();
        Map<BinaryTreeNode<Integer>, Boolean> visited = new HashMap<>();

        queue.offer(target);
        visited.put(target, true);

        int maxTime = 0;

        while (!queue.isEmpty()) {
            int size = queue.size();
            boolean burned = false;

            for (int i = 0; i < size; i++) {
                BinaryTreeNode<Integer> node = queue.poll();

                // Left child
                if (node.left != null && !visited.containsKey(node.left)) {
                    burned = true;
                    visited.put(node.left, true);
                    queue.offer(node.left);
                }

                // Right child
                if (node.right != null && !visited.containsKey(node.right)) {
                    burned = true;
                    visited.put(node.right, true);
                    queue.offer(node.right);
                }

                // Parent
                BinaryTreeNode<Integer> parent = parentMap.get(node);
                if (parent != null && !visited.containsKey(parent)) {
                    burned = true;
                    visited.put(parent, true);
                    queue.offer(parent);
                }
            }

            if (burned) maxTime++;
        }

        return maxTime;
    }

    // BFS to map parents and find target node
    private static BinaryTreeNode<Integer> bfsToMapParents(
            BinaryTreeNode<Integer> root,
            Map<BinaryTreeNode<Integer>, BinaryTreeNode<Integer>> parentMap,
            int start) {

        Queue<BinaryTreeNode<Integer>> queue = new LinkedList<>();
        queue.offer(root);

        BinaryTreeNode<Integer> target = null;

        while (!queue.isEmpty()) {
            BinaryTreeNode<Integer> node = queue.poll();

            if (node.data == start) {
                target = node;
            }

            if (node.left != null) {
                parentMap.put(node.left, node);
                queue.offer(node.left);
            }

            if (node.right != null) {
                parentMap.put(node.right, node);
                queue.offer(node.right);
            }
        }

        return target;
    }

    public static int timeToBurnTree(BinaryTreeNode<Integer> root, int start) {
        Map<BinaryTreeNode<Integer>, BinaryTreeNode<Integer>> parentMap = new HashMap<>();

        BinaryTreeNode<Integer> target =
                bfsToMapParents(root, parentMap, start);

        return findMaxDistance(parentMap, target);
    }
}
