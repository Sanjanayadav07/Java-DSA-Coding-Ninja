# 🌳 Check if Two BSTs are Identical (Using Preorder Arrays)

## 📌 Problem
Given two arrays `arr1` and `arr2` representing the **preorder traversal of two BSTs**, determine whether both BSTs are **identical**.

Return:
- `true` → if identical  
- `false` → otherwise  

---

## 🧠 Key Idea

For **BST**, preorder traversal follows:


Root → Left → Right


Important property:
- All values **less than root** belong to **left subtree**
- All values **greater than root** belong to **right subtree**

So we:
1️⃣ Compare roots  
2️⃣ Divide remaining elements into **left and right queues**  
3️⃣ Match both arrays structurally  

---

## 🛠️ Approach

### Step 1: Compare Roots
If first elements are different → return `false`.

---

### Step 2: Separate Left & Right Subtrees
For both arrays:
- If value `< root` → add to `leftQ`
- If value `> root` → add to `rightQ`

---

### Step 3: Validate Order
While traversing `arr2`:
- Check if elements match `leftQ` and `rightQ`
- If mismatch → return `false`

---

## 💻  Code

```java
import java.util.*;

public class Solution {

    public static boolean isIdenticalBST(ArrayList<Integer> arr1, ArrayList<Integer> arr2, int n) {

        int root1 = arr1.get(0);
        int root2 = arr2.get(0);

        // Compare roots
        if (root1 != root2) return false;

        ArrayDeque<Integer> leftQ = new ArrayDeque<>();
        ArrayDeque<Integer> rightQ = new ArrayDeque<>();

        // Process first array
        for (int i = 1; i < n; i++) {
            int node = arr1.get(i);

            if (node < root1) {
                leftQ.offer(node);
            } else {
                rightQ.offer(node);
            }
        }

        // Validate second array
        for (int i = 1; i < n; i++) {
            int node = arr2.get(i);

            if (node < root2) {
                if (leftQ.isEmpty() || node != leftQ.peek()) return false;
                leftQ.poll();
            }
            else if (node > root2) {
                if (rightQ.isEmpty() || node != rightQ.peek()) return false;
                rightQ.poll();
            }
        }

        return true;
    }
}
```
### ⏱️ Time Complexity
- O(N)
- Each element processed once.

### 📦 Space Complexity
- O(N)
- Using queues to store left and right subtree elements.
