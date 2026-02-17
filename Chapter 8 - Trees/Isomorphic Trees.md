# 🌳 Check If Two Binary Trees Are Flip Equivalent 

This program checks whether two Binary Trees are **Flip Equivalent**.

---

## 📌 Problem Statement

Two binary trees are considered **Flip Equivalent** if:

- They are structurally identical **OR**
- They can be made identical by swapping left and right children at some nodes.

---

## 🧠 Approach

We use **Recursion** to compare both trees.

### Base Cases:
1. If both nodes are `null` → return `true`
2. If one is `null` → return `false`
3. If node values are different → return `false`

### Recursive Cases:
At each node, check two possibilities:

1️⃣ **Without swap**
 ```
left ↔ left
right ↔ right

```
2️⃣ **With swap**
```
left ↔ right
right ↔ left

```

If either case returns `true`, trees are flip equivalent.

---
## ⏱️ Complexity Analysis
 - Time Complexity: O(n)
 - Space Complexity: O(h)
    - (h = height of tree due to recursion stack)

---
## 🧑‍💻 Code

```java
public class Solution {

    public static boolean checkTree(BinaryTreeNode<Integer> tree1,
                                    BinaryTreeNode<Integer> tree2) {

        // both null
        if (tree1 == null && tree2 == null) {
            return true;
        }

        // one null
        if (tree1 == null || tree2 == null) {
            return false;
        }

        // compare node values
        if (!tree1.data.equals(tree2.data)) {
            return false;
        }

        // same order
        boolean noSwap =
            checkTree(tree1.left, tree2.left) &&
            checkTree(tree1.right, tree2.right);

        // swapped
        boolean swap =
            checkTree(tree1.left, tree2.right) &&
            checkTree(tree1.right, tree2.left);

        return noSwap || swap;
    }
}
