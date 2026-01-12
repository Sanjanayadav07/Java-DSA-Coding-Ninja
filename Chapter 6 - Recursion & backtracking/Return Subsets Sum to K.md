# 🧩 Subsets That Sum to K 

## 📌 Problem Statement
Given an array `arr` of size `n` and an integer `k`, find **all subsets** whose sum is exactly equal to `k`.

- Each element can be chosen **at most once**
- Order of elements in a subset does not matter
- Use **recursion / backtracking**

---

## 🧠 Approach (Pick / Not Pick)
For every element at index `ind`, we have **two choices**:

1. ❌ Do not pick the element  
2. ✅ Pick the element and reduce the target sum  

When:
- `ind == arr.size()`  
  - If `target == 0`, store the current subset

This explores **all possible subsets**.

---

## 🔁 Recursion Tree Idea
At each index:
```
            []
         /      \
     not pick   pick
```

Classic **subset generation** pattern.

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(2^n)`
- **Space Complexity:** `O(n)` (recursion stack)

---

## 💻 Code

```java
import java.util.ArrayList;

public class Solution {

    public static void helper(int ind, int target,
                              ArrayList<Integer> arr,
                              ArrayList<ArrayList<Integer>> ans,
                              ArrayList<Integer> ds) {

        if (ind == arr.size()) {
            if (target == 0) {
                ans.add(new ArrayList<>(ds));
            }
            return;
        }

        // Not pick
        helper(ind + 1, target, arr, ans, ds);

        // Pick
        ds.add(arr.get(ind));
        helper(ind + 1, target - arr.get(ind), arr, ans, ds);
        ds.remove(ds.size() - 1);
    }

    public static ArrayList<ArrayList<Integer>> findSubsetsThatSumToK(
            ArrayList<Integer> arr, int n, int k) {

        ArrayList<ArrayList<Integer>> ans = new ArrayList<>();
        helper(0, k, arr, ans, new ArrayList<>());
        return ans;
    }
}
