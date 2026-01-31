# ⏳ Smart Interval (Binary Search)

This problem finds, for each interval, the **next interval** whose **start time is ≥ current interval’s end time**.  
If no such interval exists, return **-1**.

---

## 🧠 Approach Used
- 📌 **Store start time with original index**
- 🔀 **Sort intervals by start time**
- 🔍 **Binary Search** for the next valid interval
-  ✅ If such an interval is found, store its **original index**; otherwise, store **-1**.
-  🔁 Repeat this process for all intervals and return the result list.

---
## ⏱️ Time Complexity
  - O(N log N)
## 📦 Space Complexity
  - O(N)
---

## 💻 Java Code

```java
import java.util.*;

public class Solution {

    public static ArrayList<Integer> smartInterval(ArrayList<ArrayList<Integer>> intervals, int n) {

        int[][] starts = new int[n][2];

        // Store start value with original index
        for (int i = 0; i < n; i++) {
            starts[i][0] = intervals.get(i).get(0);
            starts[i][1] = i;
        }

        //  Sort intervals based on start time
        Arrays.sort(starts, (a, b) -> a[0] - b[0]);

        ArrayList<Integer> result = new ArrayList<>();

        //  For each interval, binary search next valid interval
        for (int i = 0; i < n; i++) {
            int end = intervals.get(i).get(1);

            int l = 0, r = n - 1;
            int ans = -1;

            while (l <= r) {
                int mid = l + (r - l) / 2;

                if (starts[mid][0] >= end) {
                    ans = starts[mid][1];
                    r = mid - 1;
                } else {
                    l = mid + 1;
                }
            }

            result.add(ans);
        }

        return result;
    }
}
