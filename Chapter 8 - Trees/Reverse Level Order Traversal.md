# 🌳 Reverse Level Order Traversal of Binary Tree

## 📌 Problem Statement
Given the root of a binary tree, return its **reverse level order traversal**.  
That is, traverse the tree level by level **from bottom to top** and **left to right**.

---

## 🧠 Approach
- Use a **Queue** for normal level order traversal (BFS)
- Use a **Stack** to reverse the traversal order
- Push node values into the stack while traversing
- Pop all elements from the stack into the result list

This avoids reversing the list at the end.

---

## 💻 Code

```java
import java.util.*;

public class Solution {
    public static ArrayList<Integer> reverseLevelOrder(TreeNode root) {

        if (root == null)
            return new ArrayList<>();

        Stack<Integer> st = new Stack<>();
        Queue<TreeNode> q = new LinkedList<>();

        q.add(root);

        while (!q.isEmpty()) {
            TreeNode temp = q.remove();
            st.push(temp.data);

            if (temp.left != null)
                q.add(temp.left);

            if (temp.right != null)
                q.add(temp.right);
        }

        ArrayList<Integer> ans = new ArrayList<>();
        while (!st.isEmpty()) {
            ans.add(st.pop());
        }

        return ans;
    }
}
```

---

## ⏱️ Complexity

Time Complexity: **O(N)**  
Space Complexity: **O(N)**  

---
