## 📌 Problem Statement

- You are given an integer n representing n unique Dragon Balls.
- You need to find the number of valid binary tree structures that can be formed using these n nodes, where each structure is distinct based on shape.
- Return the result modulo 1e9 + 7.
---
## 💡 Approach
### 🔑 Key Idea:

- This is a classic Catalan Number / BST Counting problem.
- We use Dynamic Programming where:
- dp[i] = number of unique binary trees with i nodes
---
## 🪜 Recurrence Relation:
- For each i nodes:
- We pick every node j as root:
- Left subtree → j nodes
- Right subtree → i - j - 1 nodes
- So:
- dp[i] = Σ (dp[j] * dp[i - j - 1])

### 🧠 Base Case:
- dp[0] = 1  → empty tree
- dp[1] = 1  → single node
---
## 🧾 Code 
```
public class Solution 
{
    public static int gokuAndDragonBalls(int n)
    {
        long mod = 1000000007;

        long[] dp = new long[n + 1];

        dp[0] = 1;
        if (n > 0) dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            dp[i] = 0;

            for (int j = 0; j < i; j++) {
                dp[i] = (dp[i] + (dp[j] * dp[i - j - 1]) % mod) % mod;
            }
        }

        return (int) dp[n];
    }
}
```
---
### ⏱️ Time Complexity
- O(n²)
- Because of nested loops for DP transitions.

### 🧠 Space Complexity
- O(n)
- For storing DP array.
---
