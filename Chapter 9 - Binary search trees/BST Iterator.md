# 🌳 BST Iterator

## 📌 Problem
Design a **BST Iterator** that supports the following operations:

- `next()` → Returns the **next smallest element** in BST  
- `hasNext()` → Returns **true** if there is a next element

The iterator should return elements in **ascending order**.

---

## 🧠 Key Idea

Important BST property:


Inorder Traversal → Sorted Order


So we:

1️⃣ Perform **inorder traversal** of BST  
2️⃣ Store elements in an **ArrayList**  
3️⃣ Use an **index pointer** to simulate iterator behavior

---

## 🛠️ Approach

### Step 1: Convert BST → Sorted List

Traverse the BST in:
Left → Root → Right
Store values in an `ArrayList`.

### Example:
- BST → Inorder → [1,2,3,4,5]
---

### Step 2: Implement Iterator Functions

#### next()
return a.get(i++)
Returns current element and moves pointer forward.

---

#### hasNext()
return i < a.size()
Checks if more elements exist.

---

## 💻 Code

```java
import java.util.*;

public class Solution {

    static class BSTIterator {

        ArrayList<Integer> a = new ArrayList<>();
        int i = 0;

        BSTIterator(TreeNode<Integer> root) {
            solve(root);
        }

        void solve(TreeNode<Integer> root) {
            if (root == null) return;

            solve(root.left);
            a.add(root.data);
            solve(root.right);
        }

        int next() {
            return a.get(i++);
        }

        boolean hasNext() {
            return i < a.size();
        }
    }
}
```
### ⏱️ Time Complexity
- Constructor (Inorder traversal) → O(N)
- next() → O(1)
- hasNext() → O(1)
### 📦 Space Complexity
- O(N)
- Because we store all BST nodes in an ArrayList.
