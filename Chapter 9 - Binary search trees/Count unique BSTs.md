# 🌳 Total Number of Unique BSTs

This program calculates the **total number of structurally unique Binary Search Trees (BSTs)**  
that can be formed using `n` distinct nodes.

---

## 📌 Problem Statement

Given:
- An integer `n`

Return:
- Total number of **unique BSTs** that can be formed using values `1 to n`.

---

## 🧠 Key Concept

The answer follows the **Catalan Number Formula**:
**C(n) = Σ C(i) * C(n-i-1)**

Where:
- `i` = root position
- Left subtree has `i` nodes
- Right subtree has `n - i - 1` nodes

---

## 💡 Why Catalan?

Because:
- Every number can act as root
- Left and right subtree combinations multiply
- Total trees = sum of all root possibilities

---
## ⏱️ Complexity Analysis
 - Time	O(n²)
 - Space	O(n)
---

## 🧑‍💻 Code

```java
public class Solution {

    public static long totalTrees(int num) {

        long mod = 1000000007;

        long[] dp = new long[num + 1];

        dp[0] = 1;  // Base case: empty tree

        for (int i = 1; i <= num; i++) {

            long sum = 0;

            for (int j = 0; j < i; j++) {
                sum = (sum + (dp[j] * dp[i - j - 1]) % mod) % mod;
            }

            dp[i] = sum;
        }

        return dp[num];
    }
}
