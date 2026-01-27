## 🧮 Square Root of a Number (Floor Value)

### 📌 Problem Statement
Given a non-negative integer `a`, find the **floor value of its square root** using Binary Search.

---

### 🔍 Approach (Binary Search)
- Search space: `0` to `a`
- For each `mid`, check:
  - If `mid * mid == a` → exact answer
  - If `mid * mid < a` → store `mid` and move right
  - Else → move left
- Return the last valid `mid` stored

---

### ⏱ Time & Space Complexity
- **Time Complexity:** `O(log a)`
- **Space Complexity:** `O(1)`

---

### 💻  Code
```java
import java.util.* ;
import java.io.*; 

public class Solution
{
    public static int squareRoot(int a)
    {
        int l = 0;
        int h = a;
        int ans = 0;

        while (l <= h) {
            int mid = l + (h - l) / 2;

            if ((long) mid * mid == a) {
                return mid;
            }

            if ((long) mid * mid < a) {
                ans = mid;
                l = mid + 1;
            } else {
                h = mid - 1;
            }
        }
        return ans;
    }
}
