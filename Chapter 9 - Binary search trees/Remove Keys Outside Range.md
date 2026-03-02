# 🌳 Remove Nodes Outside Given Range in BST

Given a BST and a range `[min, max]`,  
remove all nodes whose values lie **outside** this range.

---

## 🧠 Approach Used
- 🔁 Use **Postorder Traversal** (Left → Right → Root)
- 🌳 Process children first, then decide for current node
- ❌ If node value < min → remove node and return right subtree
- ❌ If node value > max → remove node and return left subtree
- ✅ If within range → keep the node

---
## ⏱️ Complexity:
-  Time Complexity : O(n)
-  Space Complexity : O(h)
---

## 💻 Code

```java
public class Solution {

    private static BinaryTreeNode<Integer> postOrder(BinaryTreeNode<Integer> root, int min, int max){
        if (root == null) return null;

        // Process left and right subtree first
        root.left = postOrder(root.left, min, max);
        root.right = postOrder(root.right, min, max);

        // If node value is smaller than min → discard left side
        if (root.data < min) {
            return root.right;
        }

        // If node value is greater than max → discard right side
        if (root.data > max) {
            return root.left;
        }

        // Node is within range
        return root;
    }

    public static BinaryTreeNode<Integer> removeOutsideRange(BinaryTreeNode<Integer> root, int min, int max){
        return postOrder(root, min, max);
    }
}
