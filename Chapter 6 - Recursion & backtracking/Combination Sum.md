# 🔢 Combination Sum 

This program finds **all unique combinations** of numbers from an array that sum up to a given target `B`.  
Each number can be **used multiple times**.

---

## 📌 Problem Statement

Given an integer array `ARR` and a target sum `B`, return **all unique combinations** where the chosen numbers sum to `B`.

📍 The same number may be chosen **unlimited times**.  
📍 The solution set must **not contain duplicate combinations**.

---

## 🧠 Approach (Backtracking)

We use **recursion + backtracking**:
- Sort the array to maintain order and avoid duplicates
- At each index:
  - ✅ Pick the current element (can reuse it)
  - ❌ Skip the current element and move ahead
- If `target == 0`, we store the combination

---

## 🔄 Algorithm Steps

1. Sort the input array
2. Start recursion from index `0`
3. Try including current element (do not increment index)
4. Try excluding current element (increment index)
5. Backtrack after each recursive call

---

## 💻 Code 

```java
import java.util.*;

public class Solution {

    public static List<List<Integer>> combSum(int[] ARR, int B) {
        List<List<Integer>> result = new ArrayList<>();

        Arrays.sort(ARR); // helps avoid duplicates
        solve(ARR, B, 0, new ArrayList<>(), result);

        return result;
    }

    private static void solve(int[] arr, int target, int index,
                              List<Integer> temp, List<List<Integer>> result) {

        if (target == 0) {
            result.add(new ArrayList<>(temp));
            return;
        }

        if (index >= arr.length || target < 0) return;

        // Pick current element (can be reused)
        if (arr[index] <= target) {
            temp.add(arr[index]);
            solve(arr, target - arr[index], index, temp, result);
            temp.remove(temp.size() - 1); // backtrack
        }

        // Skip current element
        solve(arr, target, index + 1, temp, result);
    }
}
