# 🍬 Distribute Candies (Binary Search + Simulation)

This problem distributes **n candies** among **k people** in increasing order  
(1, 2, 3, …) and returns how many candies each person gets.

---

## 🧠 Approach Used
- 🔍 Use Binary Search to find the maximum count such that  1 + 2 + ... + count ≤ n.
- ➕ Distribute candies from 1 to count in round-robin fashion among k people.
- 🧮 Calculate candies already used and find the remaining candies.
- 🍬 Add remaining candies to the next person.
- ✅ Return the final distribution array.
---
## ⏱️ Time Complexity
   - O(√N + N)
## 📦 Space Complexity
   - O(K)
---

## 💻 Code

```java
import java.util.*;

public class Solution {

    static int[] candies(int n, int k) {

        int[] arr = new int[k];

        // ---------- STEP 1: Binary Search (find count) ----------
        long low = 0, high = (long) Math.sqrt(2L * n), count = 0;

        while (low <= high) {
            long mid = (low + high) / 2;
            long sum = mid * (mid + 1) / 2;

            if (sum <= n) {
                count = mid;
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        // ---------- STEP 2: Distribute first 'count' candies ----------
        int person = 0;
        for (int i = 1; i <= count; i++) {
            arr[person] += i;
            person = (person + 1) % k;
        }

        // ---------- STEP 3: Remaining candies ----------
        long used = (count * (count + 1)) / 2;
        long remaining = n - used;

        if (remaining > 0) {
            arr[person] += remaining;
        }

        return arr;
    }
}
