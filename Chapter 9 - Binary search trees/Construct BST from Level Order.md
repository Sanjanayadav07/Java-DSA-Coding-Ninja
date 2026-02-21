# 🌳 Construct Balanced BST 

This program constructs a **Balanced Binary Search Tree (BST)**  
from a given list of elements.

---

## 📌 Problem Statement

Given:
- An `ArrayList<Integer>` representing node values

Construct a **Balanced Binary Search Tree (BST)**.

---

## 🧠 Approach Used

⚠️ Important Note:

The given solution:
1. Sorts the input list
2. Builds BST using middle element (like Sorted Array → BST)

So technically:
- It **does not use level order structure**
- It constructs a **Height Balanced BST from sorted array**

---

## ✅ Steps

1️⃣ Sort the input list  
2️⃣ Pick middle element as root  
3️⃣ Recursively build:
- Left subtree from left half  
- Right subtree from right half  

This ensures tree is balanced.

---
## ⏱️ Complexity Analysis
- Sorting	O(n log n)
- BST Construction	O(n)
- Total Time	O(n log n)
- Space	O(n)

---

## 🧑‍💻 Code

```java
public class Solution {

    public static BinaryTreeNode<Integer> constructBst(ArrayList<Integer> levelOrder) {

        if (levelOrder == null || levelOrder.isEmpty())
            return null;

        Collections.sort(levelOrder);

        return constructBstHelper(levelOrder, 0, levelOrder.size() - 1);
    }

    private static BinaryTreeNode<Integer> constructBstHelper(
            ArrayList<Integer> levelOrder,
            int start,
            int end) {

        if (start > end) {
            return null;
        }

        int mid = (start + end) / 2;

        BinaryTreeNode<Integer> temp =
                new BinaryTreeNode<Integer>(levelOrder.get(mid));

        temp.left = constructBstHelper(levelOrder, start, mid - 1);
        temp.right = constructBstHelper(levelOrder, mid + 1, end);

        return temp;
    }
}
