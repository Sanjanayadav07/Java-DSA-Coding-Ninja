
# Optimal Binary Search Tree (Optimal BST)

## 📌 Problem
Given:
- Sorted keys
- Search frequencies

Construct BST with minimum search cost.

---

## 🧠 Approach
Use Interval Dynamic Programming.

Try every key as root and compute:
- left subtree cost
- right subtree cost
- current frequency sum

Take minimum among all roots.

---

## 🔥 DP State

dp[i][j] =
minimum cost to build BST from i to j

---

## Code
```
import java.util.* ;
import java.io.*; 
import java.util.ArrayList;

public class Solution {

    public static int optimalCost(ArrayList<Integer> keys,
                                  ArrayList<Integer> freq,
                                  int n) {

        // dp[i][j] = minimum cost from i to j
        int[][] dp = new int[n + 2][n + 2];

        // Prefix sum for frequencies
        int[] pre = new int[n + 1];

        for (int i = 1; i <= n; i++) {
            pre[i] = pre[i - 1] + freq.get(i - 1);
        }

        // Length of subtree
        for (int len = 1; len <= n; len++) {

            // Starting index
            for (int i = 1; i + len - 1 <= n; i++) {

                int j = i + len - 1;

                // Sum of frequencies from i to j
                int sum = pre[j] - pre[i - 1];

                dp[i][j] = Integer.MAX_VALUE;

                // Try every key as root
                for (int root = i; root <= j; root++) {

                    int left = dp[i][root - 1];
                    int right = dp[root + 1][j];

                    int cost = left + right + sum;

                    dp[i][j] = Math.min(dp[i][j], cost);
                }
            }
        }

        return dp[1][n];
    }
}
```
---

## ⚡ Complexity
- Time: O(N^3)
- Space: O(N^2)
