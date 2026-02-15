# 🌳 Convert Binary Tree to Sum Tree 

This program converts a given **Binary Tree** into a **Sum Tree**.

## 📌 What is a Sum Tree?

A **Sum Tree** is a tree where:
- Each node contains the **sum of values of its left and right subtrees**
- Leaf nodes become `0`

---

## 🧠 Approach

We use **Postorder Traversal (Left → Right → Root)**.

### Steps:
1. Recursively calculate sum of left subtree
2. Recursively calculate sum of right subtree
3. Store current node value
4. Update node value = `leftSum + rightSum`
5. Return original node value to parent

Finally, perform **Preorder Traversal** to return the updated tree values.

---
## ⏱️ Complexity Analysis
 - Time Complexity: O(n)
 - Space Complexity: O(h)
   - (Recursion stack, h = height)

---

## 🧑‍💻 Code

```java
import java.util.ArrayList;

public class Solution {

    public static int sumFunction(BinaryTreeNode<Integer> root){

        if(root == null) return 0;

        // Leaf node
        if(root.left == null && root.right == null) {
            int temp = root.data;
            root.data = 0;
            return temp;
        }

        int leftValue = sumFunction(root.left);
        int rightValue = sumFunction(root.right);

        int prevNodeValue = root.data;
        root.data = leftValue + rightValue;

        return prevNodeValue;
    }

    public static void preOrder(BinaryTreeNode<Integer> root , ArrayList<Integer> ans){

        if (root != null) {
            ans.add(root.data);
            preOrder(root.left, ans);
            preOrder(root.right, ans);
        }
    }  

    public static ArrayList<Integer> sumTree(BinaryTreeNode<Integer> root) {

        int dummy = sumFunction(root);

        ArrayList<Integer> ans = new ArrayList<Integer>();
        preOrder(root, ans);

        return ans;
    }
}
