# 🌳 Create Binary Tree from Parent Array

## 📌 Problem Statement
You are given an integer array `parent[]` of size `N` where:

- `parent[i]` represents the parent of node `i`
- `parent[i] = -1` indicates the **root node**
- Each node can have **at most two children**

Construct the corresponding **Binary Tree** and return its root.

---

## 🧠 Approach
1. Create all tree nodes first.
2. Traverse the `parent[]` array:
   - If `parent[i] == -1`, mark node `i` as root
   - Else attach node `i` as:
     - left child if empty
     - otherwise right child
3. Return the root node.

---
## ⏱️ Complexity
  - Time Complexity: O(N)
  - Space Complexity: O(N)
---

## 💻 Code

```java
public class Solution {

    public static BinaryTreeNode<Integer> createTree(int[] parent) {

        int n = parent.length;
        BinaryTreeNode<Integer>[] nodes = new BinaryTreeNode[n];
        BinaryTreeNode<Integer> root = null;

        // Step 1: Create all nodes
        for (int i = 0; i < n; i++) {
            nodes[i] = new BinaryTreeNode<>(i);
        }

        // Step 2: Assign parent-child relationship
        for (int i = 0; i < n; i++) {

            if (parent[i] == -1) {
                root = nodes[i];   // Root node
            } else {
                BinaryTreeNode<Integer> parentNode = nodes[parent[i]];

                if (parentNode.left == null) {
                    parentNode.left = nodes[i];
                } else {
                    parentNode.right = nodes[i];
                }
            }
        }

        return root;
    }
}
