# 🌳 Check if Every Internal Node Has Exactly One Child (BST)

## 📌 Problem
Given the **preorder traversal** of a Binary Search Tree (BST), determine whether **every internal node has exactly one child**.

Return:
- `true` → if every internal node has exactly one child  
- `false` → otherwise

---

## 🧠 Key Idea

In a BST, if every internal node has **exactly one child**, the preorder traversal will always move **strictly in one direction** within a valid range.

We maintain a **range `[min, max]`** that each next value must satisfy.

If any value **violates the range**, then the BST structure would require **two children**, so the answer becomes `false`.

---

## 🛠️ Approach

### Step 1: Start With Root
Initialize the first element as root with full range:


min = -∞
max = +∞


---

### Step 2: Process Remaining Preorder Elements

For each next value:

1️⃣ Check if it violates the BST range


value < min OR value > max → return false


2️⃣ If value < current node  
→ It belongs to **left subtree**

Update range:

max = parent value


3️⃣ If value > current node  
→ It belongs to **right subtree**

Update range:

min = parent value


---

## 💻 Code

```java
import java.util.*;
import java.io.*;

public class Solution {

    static class Three {
        int num;
        int mini;
        int maxi;

        Three(int num, int mini, int maxi) {
            this.num = num;
            this.mini = mini;
            this.maxi = maxi;
        }
    }

    public static boolean hasExactlyOneChild(ArrayList<Integer> arr, int n) {

        Three a = new Three(arr.get(0), Integer.MIN_VALUE, Integer.MAX_VALUE);

        for (int i = 1; i < n; i++) {

            if (arr.get(i) < a.mini || arr.get(i) > a.maxi) {
                return false;
            }

            if (arr.get(i) < a.num) {
                a = new Three(arr.get(i), a.mini, a.num);
            }
            else {
                a = new Three(arr.get(i), a.num, a.maxi);
            }
        }

        return true;
    }
}
```
---
### ⏱️ Time Complexity
- O(N)
- Each element in the preorder array is processed once.

### 📦 Space Complexity
- O(1)
