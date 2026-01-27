# ♻️ Recycle Pens Problem 

Determine the **maximum number of pens** that can be recycled given available resources, using **binary search**.

---

## 📌 Problem Statement

You are given:
- `n` → total pens
- `r` → initial money
- `k` → money gained by recycling one pen
- `c` → cost to recycle one pen

Each recycled pen costs `c` money, but recycling a pen also gives back `k` money from the remaining pens.

Find the **maximum number of pens** that can be recycled.

---

## ⏱️ Time & Space Complexity

- Time Complexity: O(log n)
   - Binary search over number of pens
- Space Complexity: O(1)
   - Constant extra space
---
## 🧠 Approach (Binary Search on Answer)

- Minimum pens recycled = `0`
- Maximum pens recycled = `n`
- Use **binary search** to find the maximum feasible number of pens
- For a chosen `currPens`:
  - **Money needed** = `currPens × c`
  - **Money available** = `r + (n − currPens) × k`
- If available money ≥ needed money → try recycling more pens
- Otherwise → recycle fewer pens

---

## 💻 Code 

```java
public class Solution {

    public static int recyclePens(int n, int r, int k, int c) {

        int minPens = 0;
        int maxPens = n;
        int ans = 0;

        while (minPens <= maxPens) {
            int currPens = minPens + (maxPens - minPens) / 2;

            long amountNeeded = (long) currPens * c;
            long totalAmount = r + (long) (n - currPens) * k;

            if (totalAmount >= amountNeeded) {
                ans = currPens;
                minPens = currPens + 1;
            } else {
                maxPens = currPens - 1;
            }
        }
        return ans;
    }
}
