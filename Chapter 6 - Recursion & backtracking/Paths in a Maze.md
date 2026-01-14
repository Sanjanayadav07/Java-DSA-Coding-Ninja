# 🐭 Rat in a Maze – All Paths

## 📌 Problem Statement
You are given an `N x N` matrix where:
- `1` → path is open
- `0` → path is blocked

A rat starts from `(0,0)` and wants to reach `(N-1, N-1)`.

The rat can move in **4 directions**:
- **Down (D)**
- **Right (R)**
- **Up (U)**
- **Left (L)**

Your task is to find **all possible paths** from source to destination.

---

## 🧠 Approach (Backtracking)
- Start from `(0,0)`
- Move in all four directions
- Mark a cell as **visited** while exploring
- **Backtrack** by unmarking the cell
- Store path when destination is reached

---

## 🔁 Movement Order
```
D → R → U → L
```

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(4^(N*N))` (worst case)
- **Space Complexity:** `O(N*N)` (recursion + visited)

---

## 💻 Code

```java
import java.util.ArrayList;

public class Solution {

    public static void helper(ArrayList<ArrayList<Integer>> arr, int row, int col,
                              String path, ArrayList<String> ans) {

        int n = arr.size();

        // Out of bounds OR blocked OR visited
        if (row < 0 || col < 0 || row >= n || col >= n || arr.get(row).get(col) != 1)
            return;

        // Destination reached
        if (row == n - 1 && col == n - 1) {
            ans.add(path);
            return;
        }

        // Mark visited
        arr.get(row).set(col, -1);

        // Down
        helper(arr, row + 1, col, path + "D", ans);

        // Right
        helper(arr, row, col + 1, path + "R", ans);

        // Up
        helper(arr, row - 1, col, path + "U", ans);

        // Left
        helper(arr, row, col - 1, path + "L", ans);

        // Backtrack (unmark)
        arr.get(row).set(col, 1);
    }

    public static ArrayList<String> findAllPaths(ArrayList<ArrayList<Integer>> arr) {

        ArrayList<String> ans = new ArrayList<>();
        int n = arr.size();

        if (arr.get(0).get(0) == 0)
            return ans;

        helper(arr, 0, 0, "", ans);

        return ans;
    }
}

