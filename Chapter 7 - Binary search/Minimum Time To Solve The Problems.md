# ⏱️ Minimum Required Time (Binary Search)

This problem calculates the **minimum time required** to complete all subjects using **k solvers**,  
such that each solver works on **continuous subjects only**.

---

## 🧠 Approach Used
- 🔍 **Binary Search on Answer**
- 🤝 **Greedy allocation** of subjects to solvers

---
## ⏱️ Time Complexity
 - O(N log S)
## 📦 Space Complexity
 - O(1)

---

## 💻 Code

```java
public class Solution {

    // 🔢 Function to calculate number of solvers required
    // if maximum allowed time per solver is p
    public static long find(int s[], long p) {
        long solvers = 1;
        long currSolver = 0;

        for (int i = 0; i < s.length; i++) {
            if (currSolver + s[i] <= p) {
                currSolver += s[i];
            } else {
                currSolver = s[i];
                solvers++;
            }
        }
        return solvers;
    }

    // ⏳ Function to find minimum required time
    public static long minimumRequiredTime(int subjects[], int k) {

        long l = 0, r = 0;

        // 📏 Binary search bounds
        for (int i : subjects) {
            l = Math.max(l, i); // max subject time
            r += i;             // sum of all subject times
        }

        // 🔁 Binary Search
        while (l <= r) {
            long mid = l + (r - l) / 2;

            if (find(subjects, mid) <= k) {
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }
        return l;
    }
}
