
# Edit Distance (Levenshtein Distance)

## 📌 Problem

Given two strings:

str1
str2

Find minimum operations required to convert str1 into str2.

Allowed Operations:
1. Insert
2. Delete
3. Replace

---

## 🧠 Approach

Use Recursion + Memoization.

At every mismatch:
- Insert
- Delete
- Replace

Take minimum cost among all choices.

---

## 🔥 DP State

dp[m][n]

Minimum operations required to convert:

str1[0...m-1]
to
str2[0...n-1]

---
## Code 
```
import java.util.Arrays;

public class Solution {

    static int[][] t;

    public static int solve(String s1, String s2, int m, int n) {

        // Base Cases
        if (m == 0)
            return n;

        if (n == 0)
            return m;

        // Memoization
        if (t[m][n] != -1)
            return t[m][n];

        // Characters match
        if (s1.charAt(m - 1) == s2.charAt(n - 1)) {

            return t[m][n] = solve(s1, s2, m - 1, n - 1);

        } else {

            // Insert
            int insertC = 1 + solve(s1, s2, m, n - 1);

            // Delete
            int deleteC = 1 + solve(s1, s2, m - 1, n);

            // Replace
            int replaceC = 1 + solve(s1, s2, m - 1, n - 1);

            return t[m][n] = Math.min(insertC,
                    Math.min(deleteC, replaceC));
        }
    }

    public static int editDistance(String str1, String str2) {

        int m = str1.length();
        int n = str2.length();

        t = new int[m + 1][n + 1];

        for (int[] row : t) {
            Arrays.fill(row, -1);
        }

        return solve(str1, str2, m, n);
    }
}
```
---

## ⚡ Complexity

Time: O(M × N)

Space: O(M × N)

---
