# ⚖️ Tug of War Problem (Backtracking)

## 📌 Problem Statement
You are given an array of integers representing **strengths of players**.

Your task is to divide them into **two teams** such that:
- The size difference between the teams is **at most 1**
- The **absolute difference** of the sum of strengths of the two teams is **minimum**

Return the **minimum possible difference**.

---

## 🧠 Approach (Backtracking)
- Recursively try placing each element into:
  - **Team 1**
  - **Team 2**
- Maintain:
  - Remaining slots in both teams
  - Current sum of each team
- When both teams are filled:
  - Update the minimum difference

---

## 🔁 Recursion State
```
(index, team1_size, team2_size, sum1, sum2)
```

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(2^n)`
- **Space Complexity:** `O(n)` (recursion stack)

---

## 💻 Code

```java
import java.util.*;

public class Solution {

    static int minDiff;

    public static void solve(ArrayList<Integer> arr, int idx,
                             int t1, int t2,
                             int sum1, int sum2) {

        if (t1 == 0 && t2 == 0) {
            minDiff = Math.min(minDiff, Math.abs(sum1 - sum2));
            return;
        }

        if (idx >= arr.size())
            return;

        int val = arr.get(idx);

        // Put in Team 1
        if (t1 > 0)
            solve(arr, idx + 1, t1 - 1, t2, sum1 + val, sum2);

        // Put in Team 2
        if (t2 > 0)
            solve(arr, idx + 1, t1, t2 - 1, sum1, sum2 + val);
    }

    public static int tugOfWar(ArrayList<Integer> arr, int n) {

        minDiff = Integer.MAX_VALUE;

        int team1, team2;

        if (n % 2 == 0) {
            team1 = team2 = n / 2;
        } else {
            team1 = (n - 1) / 2;
            team2 = (n + 1) / 2;
        }

        solve(arr, 0, team1, team2, 0, 0);

        return minDiff;
    }
}
