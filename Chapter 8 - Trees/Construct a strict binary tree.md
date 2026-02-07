# 🌳 Construct Special Binary Tree from Preorder 

## 📌 Problem Statement
You are given:
- `pre[]` → preorder traversal of a binary tree  
- `typeNL[]` → character array where  
  - `'N'` = Non-leaf node  
  - `'L'` = Leaf node  

Both arrays are of the **same size**.

Your task is to **construct the Special Binary Tree** and return its root.

---

## 🧠 Approach
- Traverse the preorder array using an index (pass by reference)
- If `typeNL[index] == 'L'`  
  → create a **leaf node** and move index forward
- If `typeNL[index] == 'N'`  
  → create a node and **recursively build left and right subtrees**
- Preorder ensures root comes before its children

---
## ⏱️ Complexity Analysis
   - Time Complexity: O(N)
   - Space Complexity: O(N)
       - (Recursive stack + tree nodes)
---
## 💻 Code

```java
import java.util.*;

public class Solution {

    private static TreeNode<Integer> preorder(
            ArrayList<Integer> pre,
            ArrayList<Character> typeNL,
            int[] index) {

        // Leaf node
        if (typeNL.get(index[0]) == 'L') {
            return new TreeNode<>(pre.get(index[0]++));
        }

        // Non-leaf node
        TreeNode<Integer> root = new TreeNode<>(pre.get(index[0]++));

        root.left = preorder(pre, typeNL, index);
        root.right = preorder(pre, typeNL, index);

        return root;
    }

    public static TreeNode<Integer> constructSBT(
            ArrayList<Integer> pre,
            ArrayList<Character> typeNL) {

        int[] index = new int[]{0}; // pass by reference
        return preorder(pre, typeNL, index);
    }
}
