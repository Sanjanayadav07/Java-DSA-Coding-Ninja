# Problem Statement

Given a string `s`, count the total number of **palindromic subsequences** present in it.

A subsequence is obtained by deleting zero or more characters without changing the relative order of the remaining characters.

Since the answer can be very large, return it modulo `10^9 + 7`.

---

# Approach

## Key Idea

Use **Recursion + Memoization (Dynamic Programming)**.

Let:

dp[L][R]

represent the number of palindromic subsequences in the substring:

s[L...R]

---

## Cases

### Case 1: Characters Match

If:

s[L] == s[R]

Then every palindromic subsequence from:

- s[L+1...R]
- s[L...R-1]

can be extended.

Additionally, the pair `(s[L], s[R])` creates new palindromic subsequences.

Therefore:

dp[L][R] = 1 + dp[L+1][R] + dp[L][R-1]

---

### Case 2: Characters Do Not Match

If:

s[L] != s[R]

Then palindromic subsequences counted in both ranges are double-counted.

Apply Inclusion-Exclusion:

dp[L][R] =
dp[L+1][R]
+ dp[L][R-1]
- dp[L+1][R-1]

---

## Base Cases

### Empty String

If:

L > R

Return:

0

### Single Character

If:

L == R

Return:

1

A single character itself is a palindrome.

---

# Code

```java
import java.util.*;

public class Solution {

    public static int f(int L, int R, String s, int dp[][]) {

        if (L > R) return 0;

        if (L == R) return 1;

        if (dp[L][R] != -1) return dp[L][R];

        if (s.charAt(L) == s.charAt(R)) {
            return dp[L][R] =
                    (1 + f(L + 1, R, s, dp)
                       + f(L, R - 1, s, dp))
                    % 1000000007;
        }

        return dp[L][R] =
                (f(L + 1, R, s, dp)
                 + f(L, R - 1, s, dp)
                 - f(L + 1, R - 1, s, dp))
                % 1000000007;
    }

    public static int countPalindromicSubseq(String s) {

        int N = s.length();

        int dp[][] = new int[N][N];

        for (int row[] : dp) {
            Arrays.fill(row, -1);
        }

        return f(0, N - 1, s, dp);
    }
}
```
---
### Time Complexity

- O(N²)

- There are N × N states.
- Each state is computed only once.

### Space Complexity

- O(N²)

- DP table stores all substring states.

- Additional recursion stack: O(N)
