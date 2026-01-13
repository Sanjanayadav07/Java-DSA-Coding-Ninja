# 📍 Reach Destination (Recursion)

## 📌 Problem Statement
You are given:
- Starting point `(sx, sy)`
- Destination point `(dx, dy)`

From a point `(x, y)`, you can move to:
- `(x + y, y)`  
- `(x, x + y)`

Determine whether it is possible to **reach the destination** from the starting point.

---

## 🧠 Key Insight
Instead of moving **forward**, we work **backward** from `(dx, dy)`:

- If `dx > dy` → previous step must be `(dx - dy, dy)`
- If `dy > dx` → previous step must be `(dx, dy - dx)`
- Stop when:
  - `(dx, dy) == (sx, sy)` → ✅ reachable
  - `(dx < sx || dy < sy)` → ❌ not reachable

This is similar to the **Euclidean Algorithm (GCD logic)**.

---

## 🔁 Recursive Approach
```
(dx, dy)
├── if dx == dy → stop
├── if dx > dy → (dx - dy, dy)
├── if dy > dx → (dx, dy - dx)
└── if equals start → true
```

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(log(max(dx, dy)))`
- **Space Complexity:** `O(log(max(dx, dy)))` (recursive stack)

---

## 💻 Code

```java
public class Solution {
    public static boolean reachDestination(int sx, int sy, int dx, int dy) {

        if (sx == dx && sy == dy)
            return true;

        if (dx < sx || dy < sy)
            return false;

        if (dx > dy)
            return reachDestination(sx, sy, dx - dy, dy);

        if (dy > dx)
            return reachDestination(sx, sy, dx, dy - dx);

        return false;
    }
}
