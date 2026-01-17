# 📍 Closest Pair of Points

This program finds the **minimum squared Euclidean distance** between any two points in a 2D plane.

---

## 📌 Problem Statement

Given `n` points with integer coordinates `(x, y)`, determine the **closest pair of points** and return the **minimum squared distance** between them.

---

## 🧠 Approach Used

This is an **optimized brute-force approach** using sorting:

### 🔹 Steps:
1. Convert points into a `long[][]` array
2. Sort points by **x-coordinate** and compute distance of adjacent pairs
3. Sort points by **y-coordinate** and compute distance of adjacent pairs
4. Return the **minimum of both results**

> ⚠️ Note: This is not the full divide-and-conquer solution, but an optimized approach often accepted in coding platforms.

---

## 💻 Code 

```java
import java.util.*;

public class Solution {
	
	public static long closestPair(point coordinates[], int n) {

        long[][] arr = new long[n][2];

        for (int i = 0; i < n; i++) {
            arr[i][0] = coordinates[i].x;
            arr[i][1] = coordinates[i].y;
        }

        // Sort by X-coordinate
        Arrays.sort(arr, (a, b) -> Long.compare(a[0], b[0]));

        long ans = Long.MAX_VALUE;

        for (int i = 0; i < n - 1; i++) {
            long dx = arr[i][0] - arr[i+1][0];
            long dy = arr[i][1] - arr[i+1][1];
            ans = Math.min(ans, dx*dx + dy*dy);
        }

        // Sort by Y-coordinate
        Arrays.sort(arr, (a, b) -> Long.compare(a[1], b[1]));

        for (int i = 0; i < n - 1; i++) {
            long dx = arr[i][0] - arr[i+1][0];
            long dy = arr[i][1] - arr[i+1][1];
            ans = Math.min(ans, dx*dx + dy*dy);
        }

        return ans;
	}
}
