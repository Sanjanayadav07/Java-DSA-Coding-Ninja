## 📌 Problem Statement

- Given two strings s and r of the same length, determine whether r is a scrambled string of s.

### 🔄 Scrambled String Definition:

- A string can be transformed by:
  - Dividing it into two non-empty substrings
  - Recursively swapping or not swapping the substrings

- Return true if r is a scrambled version of s, otherwise false.
---
## 💡 Approach
### 🔑 Key Idea:

- Use Recursion + Memoization (DP)

- At every split index i, we check two possibilities:
   - Swapped case
   - Not swapped case
---
## 🪜 Recurrence Logic:

- For every partition i:

### Swapped:
```
s[0...i]   ↔   r[n-i...n]
s[i...n]   ↔   r[0...n-i]
```
### Not Swapped:
```
s[0...i]   ↔   r[0...i]
s[i...n]   ↔   r[i...n]
```
- If any partition satisfies → return true
---
## 🧠 Memoization:

- We store results of subproblems:

- key = s + "-" + r

- This avoids recomputation → makes solution efficient.
---
## 🧾 Code 
```
import java.util.*;

public class Solution {

    static HashMap<String, Boolean> mp = new HashMap<>();

    public static boolean solve(String s, String r) {

        if (s.equals(r)) return true;

        if (s.length() != r.length()) return false;

        String key = s + "-" + r;

        if (mp.containsKey(key)) {
            return mp.get(key);
        }

        int n = s.length();
        boolean result = false;

        for (int i = 1; i < n; i++) {

            // swapped case
            boolean swapped =
                    solve(s.substring(0, i), r.substring(n - i)) &&
                    solve(s.substring(i), r.substring(0, n - i));

            if (swapped) {
                result = true;
                break;
            }

            // not swapped case
            boolean notSwapped =
                    solve(s.substring(0, i), r.substring(0, i)) &&
                    solve(s.substring(i), r.substring(i));

            if (notSwapped) {
                result = true;
                break;
            }
        }

        mp.put(key, result);
        return result;
    }

    public static boolean isScramble(String s, String r) {
        mp.clear();
        return solve(s, r);
    }
}
```
---
### ⏱️ Time Complexity
- O(n^4)
- Why?
   - O(n^3) states (all substring pairs)
- For each state, we try n partitions
### 🧠 Space Complexity
- O(n^3)
- Memoization map stores substring pairs
