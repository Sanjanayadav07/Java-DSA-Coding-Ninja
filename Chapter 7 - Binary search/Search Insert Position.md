# 🔍 Search Insert Position 

## 📌 Problem Statement
Given a **sorted array** and a target value `m`, return the **index if the target is found**.  
If not found, return the index where it would be **inserted in order**.

---

## 🧠 Approach 
- Use binary search on the sorted array
- If element equals target → return index
- If not found → return the position where it should be inserted (`l`)

---

## 💻 Code

```java
public class Solution {
    public static int searchInsert(int[] arr, int m) {
        int l = 0;
        int h = arr.length - 1;

        while (l <= h) {
            int mid = l + (h - l) / 2;

            if (arr[mid] == m) {
                return mid;
            } else if (arr[mid] > m) {
                h = mid - 1;
            } else {
                l = mid + 1;
            }
        }
        return l;
    }
}
```
---

## ⏱️ Complexity
- Time Complexity: **O(log N)**  
- Space Complexity: **O(1)**
---
