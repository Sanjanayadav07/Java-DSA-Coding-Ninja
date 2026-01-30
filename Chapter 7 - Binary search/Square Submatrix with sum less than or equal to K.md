# 🟦 Largest Square Submatrix (Binary Search + Prefix Sum)

This problem finds the **largest square submatrix** such that the **sum of its elements is ≤ k**.  
It uses **Prefix Sum** for fast submatrix sum calculation and **Binary Search** on square size.

---

## 🧠 Approach Used
- 📊 **2D Prefix Sum** to calculate submatrix sum in O(1)
- 🔍 **Binary Search on square size**
- 🔁 **Sliding window over matrix**

---
## ⏱️ Time Complexity
  - O(N × M × log(min(N, M)))

## 📦 Space Complexity
  - O(N × M)

---

## 💻 Java Code

```java
import java.util.*;

public class Solution {

    public static int largestSquareSubmatrix(int[][] mat, int n, int m, int k) {

        int largestSize = 0;

        //  Prefix Sum Matrix
        int[][] prefixSum = new int[n + 1][m + 1];

        //  Build prefix sum
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                prefixSum[i][j] = mat[i - 1][j - 1]
                        + prefixSum[i - 1][j]
                        + prefixSum[i][j - 1]
                        - prefixSum[i - 1][j - 1];
            }
        }

        //  Binary search on square size
        int left = 0, right = Math.min(n, m);

        while (left <= right) {
            int mid = left + (right - left) / 2;
            boolean found = false;

            //  Check all mid x mid submatrices
            for (int i = 1; i <= n - mid + 1 && !found; i++) {
                for (int j = 1; j <= m - mid + 1; j++) {

                    int sum = prefixSum[i + mid - 1][j + mid - 1]
                            - prefixSum[i + mid - 1][j - 1]
                            - prefixSum[i - 1][j + mid - 1]
                            + prefixSum[i - 1][j - 1];

                    if (sum <= k) {
                        found = true;
                        break;
                    }
                }
            }

            if (found) {
                largestSize = mid;
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return largestSize * largestSize;
    }
}
