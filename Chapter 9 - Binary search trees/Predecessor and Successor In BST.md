# 🌳 Predecessor and Successor in BST

## 📌 Problem
Given a **Binary Search Tree (BST)** and a `key`, find:

- **Predecessor (pre)** → Largest value **smaller than key**
- **Successor (suc)** → Smallest value **greater than key**

Return them in an ArrayList:

[predecessor, successor]


If not found → return `-1`.

---

## 🧠 Key Idea

Using **BST Property**:


Left subtree → smaller values
Right subtree → greater values


So while traversing:

### Successor
- Move left when node value > key  
- Store possible successor

### Predecessor
- Move right when node value < key  
- Store possible predecessor

---

## 🛠️ Approach

### Step 1: Find Successor

Traverse BST:


if key < root.data
suc = root.data
move left
else
move right


---

### Step 2: Find Predecessor

Traverse BST again:


if key > root.data
pre = root.data
move right
else
move left


---

## 💻 Code

```java
import java.util.*;

public class Solution {

    public static ArrayList<Integer> findPreSuc(binaryTreeNode root, int key) {

        int pre = -1;
        int suc = -1;

        binaryTreeNode root2 = root;

        // Find Successor
        while (root != null) {

            if (key > root.data) {
                root = root.right;
            } 
            else if (key < root.data) {
                suc = root.data;
                root = root.left;
            } 
            else {
                root = root.right;
            }
        }

        // Find Predecessor
        while (root2 != null) {

            if (key > root2.data) {
                pre = root2.data;
                root2 = root2.right;
            } 
            else if (key < root2.data) {
                root2 = root2.left;
            } 
            else {
                root2 = root2.left;
            }
        }

        ArrayList<Integer> ans = new ArrayList<>(Arrays.asList(pre, suc));
        return ans;
    }
}
```
### ⏱️ Time Complexity
- O(H)
- Where:

  - H = height of BST
  - Worst case (skewed tree): O(N)
### 📦 Space Complexity
- O(1)
- Only a few variables are used.
