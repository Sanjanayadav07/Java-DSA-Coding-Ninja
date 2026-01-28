## 🐄 Aggressive Cows Problem

### 📌 Problem Statement
You are given positions of `n` stalls and `k` cows.  
Place the cows in the stalls such that the **minimum distance between any two cows is maximized**.

Return the **largest minimum distance possible**.

---

### 🔍 Approach (Binary Search on Answer)
- Sort the stall positions
- Minimum distance (`start`) = `1`
- Maximum distance (`end`) = `lastStall - firstStall`
- Use **binary search** on distance:
  - For a given distance `mid`, check if it’s possible to place all `k` cows
  - If possible → store answer & try larger distance
  - Else → reduce distance

---

### ⏱ Time & Space Complexity
- **Time Complexity:** `O(n log n)`
  - Sorting: `O(n log n)`
  - Binary Search with feasibility check: `O(n log n)`
- **Space Complexity:** `O(1)`

---

### 💻 Code
```java
import java.util.*;

public class Solution {

    public static boolean isPossible(int[] stalls, int k, int n, int minDist) {
        int count = 1;                 // first cow at first stall
        int lastPos = stalls[0];

        for (int i = 1; i < n; i++) {
            if (stalls[i] - lastPos >= minDist) {
                count++;
                lastPos = stalls[i];
            }
            if (count == k) {
                return true;
            }
        }
        return false;
    }

    public static int aggressiveCows(int[] stalls, int k) {

        Arrays.sort(stalls);
        int n = stalls.length;

        int s = 1;
        int e = stalls[n - 1] - stalls[0];
        int ans = -1;

        while (s <= e) {
            int mid = s + (e - s) / 2;

            if (isPossible(stalls, k, n, mid)) {
                ans = mid;       // valid distance
                s = mid + 1;     // try bigger distance
            } else {
                e = mid - 1;     // reduce distance
            }
        }
        return ans;
    }
}
