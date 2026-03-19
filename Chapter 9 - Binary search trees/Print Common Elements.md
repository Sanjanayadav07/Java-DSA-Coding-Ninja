# 🌳 Common Elements in Two BSTs

## 📌 Problem
Given two **Binary Search Trees (BSTs)**, find all the **common elements** present in both trees.

Return the result as an **ArrayList**.

---

## 🧠 Key Idea

We use:
- 🔁 **Inorder Traversal** (to visit all nodes)
- 🧠 **HashSet** (to store elements of first BST)

---

## 🛠️ Approach

### Step 1: Traverse First BST
- Store all elements in a **HashSet**

---

### Step 2: Traverse Second BST
- For each node:
  - If element exists in set → add to result list ✅
  - Else → ignore

---

## 💻 Code

```java
import java.util.*;

public class Solution 
{
    public static ArrayList<Integer> commonElements(BinaryTreeNode<Integer> ptr1, BinaryTreeNode<Integer> ptr2) 
    {
        Set<Integer> set = new HashSet<>();
        ArrayList<Integer> list = new ArrayList<>();

        // Store elements of first BST
        store(ptr1, set);

        // Check elements of second BST
        findCommon(ptr2, set, list);

        return list; 
    }

    // Store all elements of first BST
    static void store(BinaryTreeNode<Integer> root, Set<Integer> set){
        if(root == null) return;

        store(root.left, set);
        set.add(root.data);
        store(root.right, set);
    }

    // Find common elements
    static void findCommon(BinaryTreeNode<Integer> root, Set<Integer> set, ArrayList<Integer> list){
        if(root == null) return;

        findCommon(root.left, set, list);

        if(set.contains(root.data)){
            list.add(root.data);
        }

        findCommon(root.right, set, list);
    }
}
```
### ⏱️ Time Complexity
- O(N + M)
- Where:
- N = nodes in first BST
- M = nodes in second BST

### 📦 Space Complexity
- O(N)
- HashSet stores elements of first BST
