# 🌳 Find Closest Element in BST

## 📌 Problem
Given a **Binary Search Tree (BST)** and an integer `k`, find the node value in the BST that is **closest to k**.

If two values are equally close, return the **smaller value**.

---

## 🧠 Key Idea

Since it is a **BST**, we can use its property:


If node.data > k → go left
If node.data < k → go right


This helps us avoid searching the entire tree.

---

## 🛠️ Approach

### Step 1: Maintain Two Values

We store:


ans[0] → minimum difference found so far
ans[1] → closest value


Initial values:


ans = {Integer.MAX_VALUE, Integer.MAX_VALUE}


---

### Step 2: Traverse Using BST Property

At each node:

1️⃣ Calculate difference:

diff = abs(node.data - k)


2️⃣ Update answer if:
- `diff < ans[0]`
- OR `diff == ans[0]` and current value is smaller

3️⃣ Move:
- Left if `node.data > k`
- Right if `node.data < k`

---

## 💻 Code

```java
public class Solution {

    private static void solve(TreeNode<Integer> node, int k, int[] ans) {

        if (node == null) return;

        int diff = Math.abs(node.data - k);

        // Update closest value
        if (diff < ans[0] || (diff == ans[0] && node.data < ans[1])) {
            ans[0] = diff;
            ans[1] = node.data;
        }

        // BST property
        if (node.data > k) {
            solve(node.left, k, ans);
        } 
        else if (node.data < k) {
            solve(node.right, k, ans);
        }
    }

    public static int findClosestElement(TreeNode<Integer> node, int k) {

        int[] ans = new int[]{Integer.MAX_VALUE, Integer.MAX_VALUE};

        solve(node, k, ans);

        return ans[1];
    }
}
```
---
### ⏱️ Time Complexity
- O(H)

### 📦 Space Complexity
- O(H)

