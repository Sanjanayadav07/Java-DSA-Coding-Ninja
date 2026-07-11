# Problem Statement

Given three strings `a`, `b`, and `c`, determine whether `c` is formed by interleaving `a` and `b`.

An interleaving of two strings preserves the relative order of characters from each string.

Return:

- `true` if `c` is an interleaving of `a` and `b`
- `false` otherwise

---

# Approach

## Key Idea

Use **Recursion + Memoization (Dynamic Programming)**.

At any position `(i, j)`:

- `i` characters have been taken from string `a`
- `j` characters have been taken from string `b`
- Current position in `c` is `i + j`

We try to match the next character of `c` with:

1. Current character of `a`
2. Current character of `b`

If either choice leads to a valid interleaving, the answer is true.

---

## DP State

Let:

dp[i][j]

represent whether it is possible to form the remaining part of `c`
using:

- `a[i...]`
- `b[j...]`

---

## Recurrence

### Take Character From `a`

If:

a[i] == c[i+j]

Then:

check(i+1, j)

---

### Take Character From `b`

If:

b[j] == c[i+j]

Then:

check(i, j+1)

---

### Result

If either path succeeds:

dp[i][j] = true

Otherwise:

dp[i][j] = false

---

## Base Cases

### Successfully Used All Characters

If:

i == m AND j == n

Return true.

### Length Mismatch

If:

m + n != c.length()

Return false immediately.

---

# Code

```java
public class Solution {

    static int m, n, N;
    static Boolean[][] dp;

    static boolean check(String a, String b, String c, int i, int j) {

        if (i >= m && j >= n && i + j >= N) {
            return true;
        }

        if (i + j >= N) {
            return false;
        }

        if (dp[i][j] != null) {
            return dp[i][j];
        }

        boolean result = false;

        if (i < m && a.charAt(i) == c.charAt(i + j)) {
            result = check(a, b, c, i + 1, j);
        }

        if (result) {
            return dp[i][j] = true;
        }

        if (j < n && b.charAt(j) == c.charAt(i + j)) {
            result = check(a, b, c, i, j + 1);
        }

        return dp[i][j] = result;
    }

    public static boolean isInterleave(String a, String b, String c) {

        m = a.length();
        n = b.length();
        N = c.length();

        if (m + n != N) {
            return false;
        }

        dp = new Boolean[m + 1][n + 1];

        return check(a, b, c, 0, 0);
    }
}
```
---
### Time Complexity
- O(M × N)
- Each state (i, j) is computed only once because of memoization.
  
### Space Complexity
- O(M × N)
- DP table stores all states.
