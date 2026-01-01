
## 📌 Problem Statement
You are given an array `arr` containing `n` integers and an integer `num`.

Your task is to check whether `num` is present in the array.

- If `num` is found, return the **0-based index of its first occurrence**
- If `num` is not found, return **-1**

---

## 🧠 Approach
- Traverse the array from index `0` to `n - 1`
- Compare each element with `num`
- Return the index when found
- If not found, return `-1`

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## 💻 Java Implementation

```java
import java.util.*;

public class Solution {
    public static int linearSearch(int n, int num, int[] arr) {
        for (int idx = 0; idx < n; idx++) {
            if (arr[idx] == num) {
                return idx;
            }
        }
        return -1;
    }
}

