# 🔁 Print Series Without Using Loop 

## 📌 Problem Statement
Given two integers `N` and `K`, print a series starting from `N` such that:

- Decrease the value by `K` until it becomes **≤ 0**
- Then increase the value by `K` back to `N`
- **Loops are not allowed**
- Use **recursion only**

---

## 🧠 Approach (Recursion)
- Start from `N`
- Keep subtracting `K` and add values to the list
- Once `n <= 0`, stop recursion
- While returning from recursion, add the values again to form the increasing part

- This naturally forms:
- N → N-K → N-2K → ... → 0/negative → ... → N
---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(N / K)`
- **Space Complexity:** `O(N / K)` (recursion stack)

---

## 💻 Code

```java
import java.util.*;

public class Solution {

    public static List<Integer> printSeries(int n, int k) {
        List<Integer> list = new ArrayList<>();
        printSeries(n, n, k, list, true);
        return list;
    }

    public static void printSeries(int n, int N, int k, List<Integer> list, boolean flag) {
        list.add(n);

        if (n <= 0)
            return;

        printSeries(n - k, N, k, list, flag);
        list.add(n);
    }
}
