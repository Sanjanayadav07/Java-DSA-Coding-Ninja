# 🔍 First One in Infinite Binary Array 

## 🧩 Problem Statement
You are given access to an **infinite binary array** containing only `0`s followed by `1`s.  
You cannot access the array directly. Instead, you can query elements using:
Your task is to find the **index of the first occurrence of `1`**.

---

## 💡 Approach

Because the array size is unknown:

### 1️⃣ Exponential Search
- Start with a small range
- Keep doubling `high` until `Runner.get(high) == 1`

### 2️⃣ Binary Search
- Apply binary search in the range `[low, high]`
- Find the **leftmost index** containing `1`

---

## 🧠 Algorithm
1. Initialize `low = 0`, `high = 1`
2. Increase `high` exponentially until value becomes `1`
3. Apply binary search in the found range
4. Return the first index where value is `1`

---
## ⏱️ Time & Space Complexity

### ⏳ Time Complexity
- **Exponential Search:** `O(log N)`
- **Binary Search:** `O(log N)`

➡️ **Overall Time Complexity:** `O(log N)`

> `N` = index of the first occurrence of `1`

---

### 🧠 Space Complexity
- Uses only constant variables

 ➡️ **Space Complexity:** `O(1)`
---

## 💻  Code

```java
public class Solution {

    public static long firstOne() {
        long low = 0;
        long high = 1;

        // Exponential search to find range
        while (Runner.get(high) == 0) {
            low = high;
            high = high * 2;
        }

        // Binary search to find first 1
        long ans = high;
        while (low <= high) {
            long mid = low + (high - low) / 2;

            if (Runner.get(mid) == 1) {
                ans = mid;
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return ans;
    }
}

