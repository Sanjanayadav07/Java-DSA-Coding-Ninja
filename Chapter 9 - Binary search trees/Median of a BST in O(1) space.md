# 🌳 Median of BST

## 📌 Problem
Given a **Binary Search Tree (BST)**, find the **median of all nodes**.

Median definition:

- If number of nodes is **odd** → middle element  
- If number of nodes is **even** → average of two middle elements

---

## 🧠 Key Idea

- Important BST property:
- Inorder Traversal of BST → Sorted Order
- So we can:
  - 1. Convert BST → **sorted list**
  - 2. Find median from that list

---

## 🛠️ Approach

### Step 1: Perform Inorder Traversal
- Traverse the BST in:
  - Left → Root → Right
- Store values in an **ArrayList**.
- Example:
- BST → Inorder → [1,2,3,4,5]


---

### Step 2: Find Median

- Let: n = size of list


### Case 1: Odd number of nodes


- median = list[n/2]


### Case 2: Even number of nodes


- median = (list[n/2 - 1] + list[n/2]) / 2


---

## 💻 Code

```java
import java.util.ArrayList;

public class Solution {

    private static void inorder(TreeNode<Integer> node, ArrayList<Integer> list) {
        if (node == null) return;

        inorder(node.left, list);
        list.add(node.data);
        inorder(node.right, list);
    }

    public static int medianBST(TreeNode<Integer> root) {

        ArrayList<Integer> list = new ArrayList<>();

        // Convert BST → Sorted List
        inorder(root, list);

        int n = list.size();

        // Even nodes
        if (n % 2 == 0) {
            return (list.get(n / 2 - 1) + list.get(n / 2)) / 2;
        }
        // Odd nodes
        else {
            return list.get(n / 2);
        }
    }
}
```
---
### ⏱️ Time Complexity
 - O(N)
 - Inorder traversal visits every node once.

### 📦 Space Complexity
- O(N)
