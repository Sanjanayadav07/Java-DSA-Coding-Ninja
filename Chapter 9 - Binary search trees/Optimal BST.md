# 🌳 Optimal Binary Search Tree (OBST)

This program calculates the **minimum search cost** of an  
Optimal Binary Search Tree (OBST).

---

## 📌 Problem Statement

Given:
- `keys[]` → Sorted keys of BST  
- `freq[]` → Frequency of each key  

Construct a Binary Search Tree such that  
👉 **Expected search cost is minimum**.

Return the minimum cost.

---

## 🧠 Concept

Search cost of a BST depends on:

Cost =  
```
Σ (frequency × depth)

```
To minimize cost:
- Frequently searched keys should be closer to root.
- Less frequent keys should be deeper.

---

## 💡 Approach (Dynamic Programming)

We use:


```
dp[i][j] = minimum cost of BST using keys from i to j

```
### Steps:

1️⃣ Use Prefix Sum (`pre[]`) for fast frequency range sum  
2️⃣ Try every key as root  
3️⃣ Choose minimum cost combination  

---

## 🧑‍💻 Code

```java
public class Solution {

    public static int optimalCost(ArrayList<Integer> keys,
                                  ArrayList<Integer> freq,
                                  int n) {

        int[][] dp = new int[n + 2][n + 2];
        int[] pre = new int[n + 2];

        // Prefix sum of frequencies
        for (int i = 1; i <= n; i++) {
            pre[i] = pre[i - 1] + freq.get(i - 1);
        }

        pre[n + 1] = pre[n];

        // Length of range
        for (int len = 0; len < n; len++) {

            for (int start = 1, end = 1 + len;
                 start <= n - len;
                 start++, end++) {

                if (len == 0) {
                    dp[start][end] = freq.get(start - 1);
                } else {

                    int ans = Integer.MAX_VALUE;

                    for (int root = start; root <= end; root++) {

                        int cost =
                                freq.get(root - 1)
                                + dp[start][root - 1]
                                - pre[start - 1] + pre[root - 1]
                                + dp[root + 1][end]
                                + pre[end] - pre[root];

                        ans = Math.min(ans, cost);
                    }

                    dp[start][end] = ans;
                }
            }
        }

        return dp[1][n];
    }
}
