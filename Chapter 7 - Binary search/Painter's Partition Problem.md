## 🎨 Painter's Partition Problem

### 📌 Problem Statement
You are given an array `boards` where each element represents the length of a board.  
There are `k` painters available, and each painter paints **contiguous boards only**.

Each unit length of board takes **1 unit time** to paint.

Find the **minimum time** required to paint all boards such that:
- Each board is painted by exactly one painter
- Each painter paints continuous boards

---

### 🔍 Approach (Binary Search on Answer)
- Minimum possible time = **max board length**
- Maximum possible time = **sum of all boards**
- Apply **binary search** on the time:
  - For a given `mid` (max allowed time), check if boards can be painted using `k` painters
  - If possible → try smaller time
  - Else → increase time

---

### ⏱ Time & Space Complexity
- **Time Complexity:** `O(n log(sum))`
  - Binary search over time range
  - Linear feasibility check
- **Space Complexity:** `O(1)`


---

### 💻 Code
```java
import java.util.ArrayList;

public class Solution {

    // Helper function to check if painting is possible
    private static boolean isPossible(ArrayList<Integer> boards, int k, int maxAllowedTime) {
        int painters = 1;
        int time = 0;

        for (int i = 0; i < boards.size(); i++) {
            if (boards.get(i) > maxAllowedTime) {
                return false;
            }

            if (time + boards.get(i) <= maxAllowedTime) {
                time += boards.get(i);
            } else {
                painters++;
                time = boards.get(i);
            }
        }
        return painters <= k;
    }

    // Function to find minimum time required
    public static int findLargestMinDistance(ArrayList<Integer> boards, int k) {
        int sum = 0;
        int maxVal = Integer.MIN_VALUE;

        for (int board : boards) {
            sum += board;
            maxVal = Math.max(maxVal, board);
        }

        int start = maxVal;
        int end = sum;
        int ans = -1;

        while (start <= end) {
            int mid = start + (end - start) / 2;

            if (isPossible(boards, k, mid)) {
                ans = mid;
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }
        return ans;
    }
}
