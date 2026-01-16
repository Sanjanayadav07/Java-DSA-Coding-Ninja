# 🔀 Split Array into K Equal Sum Subsets 

## 📌 Problem Statement
Given an integer array `arr[]` and an integer `K`, determine whether it is possible to **divide the array into K non-empty subsets** such that:

- Each subset has the **same sum**
- Every element belongs to **exactly one subset**

Return `true` if possible, otherwise `false`.

---

## 🧠 Key Insight
- Let total sum = `S`
- For valid partition:
  - `S % K == 0`
  - Each subset must sum to `S / K`

This is a **classic backtracking + subset partition** problem.

---

## 🔁 Approach (Backtracking)
1. Calculate total sum
2. If `totalSum % K != 0` → ❌ not possible
3. Recursively try to build subsets of sum = `totalSum / K`
4. Use a `visited[]` array to ensure:
   - Each element is used **only once**
5. When one subset is completed:
   - Reduce `K` and start forming the next subset

---

## 🧩 Recursive State
- (index, targetSum, visited[], remainingSubsets, currentSum)

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(K * 2^N)` (worst case)
- **Space Complexity:** `O(N)` (visited + recursion stack)

---

## 💻 Code

```java
import java.util.*;
import java.io.*;

public class Solution {

    static boolean rec(int idx, int div, int arr[],
                       boolean vis[], int k, int csum) {

        if (k == 0) return true;
        if (csum > div) return false;

        if (csum == div)
            return rec(0, div, arr, vis, k - 1, 0);

        for (int i = idx; i < arr.length; i++) {

            if (vis[i]) continue;

            vis[i] = true;

            if (rec(i + 1, div, arr, vis, k, csum + arr[i]))
                return true;

            vis[i] = false; // backtrack
        }

        return false;
    }

    static boolean splitArray(int arr[], int K) {

        int totalSum = 0;
        int n = arr.length;

        for (int x : arr)
            totalSum += x;

        if (totalSum < K || totalSum % K != 0)
            return false;

        int target = totalSum / K;
        boolean[] visited = new boolean[n];

        return rec(0, target, arr, visited, K, 0);
    }
}
