# 🌳 Distance Between Two Nodes in BST

## 📌 Problem
Given a **Binary Search Tree (BST)** and two nodes,  
find the **distance between them** (number of edges).

---

## 🧠 Key Idea

👉 Use **LCA (Lowest Common Ancestor)**


- Distance = dist(LCA → node1) + dist(LCA → node2)


---

## ⚡ Why BST Helps?

👉 BST property:

- left < root < right


- ✔ Helps find LCA faster (no need to search whole tree)

---

## 🛠️ Approach

### 🔹 Step 1: Find LCA

- If both nodes < root → go left  
- If both nodes > root → go right  
- Otherwise → current node is LCA  

---

### 🔹 Step 2: Find Distance

- 👉 Count steps from LCA to each node  

---

## 💻 Code

```java
public class Solution {

    // Find LCA in BST
    public static BinaryTreeNode<Integer> findLCA(BinaryTreeNode<Integer> root, int node1, int node2) {
        
        if (root == null) return null;

        if (root.data > node1 && root.data > node2) {
            return findLCA(root.left, node1, node2);
        }

        if (root.data < node1 && root.data < node2) {
            return findLCA(root.right, node1, node2);
        }

        return root; // LCA found
    }

    // Distance from root to given value
    public static int distanceFromRoot(BinaryTreeNode<Integer> root, int value) {

        if (root.data == value) return 0;

        if (value < root.data) {
            return 1 + distanceFromRoot(root.left, value);
        } else {
            return 1 + distanceFromRoot(root.right, value);
        }
    }

    public static int distanceBetween2(BinaryTreeNode<Integer> root, int node1, int node2) {

        BinaryTreeNode<Integer> lca = findLCA(root, node1, node2);

        int d1 = distanceFromRoot(lca, node1);
        int d2 = distanceFromRoot(lca, node2);

        return d1 + d2;
    }
}
```
---
### ⏱️ Time Complexity
- O(H)
- H = height of BST
- Balanced BST → O(log N)
### 📦 Space Complexity
- O(H)
- Recursive calls
