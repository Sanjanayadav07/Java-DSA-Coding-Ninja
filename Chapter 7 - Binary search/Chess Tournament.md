# 🧠 Chess Tournament 

Find the **maximum minimum distance** between players placed at given positions.

---

## 📌 Problem Summary

Given:
- Stall/position array
- Number of players `c`

Goal:
> Place players such that the **minimum distance between any two players is maximized**.

---

## ⚙️ Approach

- Sort the positions array
- Apply **Binary Search on distance**
- For each distance → check if placement is possible (greedy)
- If possible → try larger distance
- If not → reduce distance

---

## 🔍 Greedy Check Logic

We place first player at first position.  
Then place next player only if distance ≥ required.

---

## 💻 Java

```java
import java.util.Arrays;

public class Solution {

    private static boolean canPlace(int[] pos, int c, int dist) {
        int players = 1;
        int last = pos[0];

        for (int i = 1; i < pos.length; i++) {
            if (pos[i] - last >= dist) {
                players++;
                last = pos[i];
            }

            if (players >= c) return true;
        }

        return false;
    }

    public static int chessTournament(int[] positions, int n, int c) {
        Arrays.sort(positions);

        int low = 1;
        int high = positions[n-1] - positions[0];
        int ans = 0;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (canPlace(positions, c, mid)) {
                ans = mid;
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return ans;
    }
}
```

---

## 🧪 Example

```python
positions = [1, 2, 4, 8, 9]
c = 3
```

### ✅ Output

```
3
```

---

## 📊 Dry Run

| Distance Try | Placement Possible | Action |
|---------------|-------------------|----------|
| 4 | ❌ | decrease |
| 2 | ✅ | increase |
| 3 | ✅ | increase |
| 4 | ❌ | stop |

**Final Answer = 3**

---

## ⏱ Complexity

**Time:** `O(n log range)`  
**Space:** `O(1)`

---

⭐ Binary Search on Answer Pattern Problem
