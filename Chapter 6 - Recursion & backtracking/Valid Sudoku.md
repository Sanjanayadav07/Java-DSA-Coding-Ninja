# 🧩 Sudoku Solver (Backtracking)

## 📌 Problem Statement
Given a partially filled **9×9 Sudoku board**, determine whether it is **solvable**.

Rules:
- Each number **1–9** must appear **exactly once**
  - in each row
  - in each column
  - in each 3×3 sub-grid
- Empty cells are represented by `0`

---

## 🧠 Approach (Backtracking)
This solution uses **DFS + backtracking**:

1. Traverse the board to find an empty cell (`0`)
2. Try placing numbers from `1` to `9`
3. Check if the number is **safe**:
   - Row check
   - Column check
   - 3×3 sub-grid check
4. If valid → place the number and recurse
5. If it leads to a dead end → **backtrack**

If the board fills completely, the Sudoku is solvable ✅

---

## 🔁 Algorithm Flow
```
Find empty cell
├── Try 1..9
│ ├── Safe? → Place
│ │ └── Recurse
│ └── Not safe → Skip
└── No number fits → Backtrack
```

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(9^(empty cells))` (worst case)
- **Space Complexity:** `O(81)` recursion stack (max)

---

## 💻 Code

```java
public class Solution {

    public static boolean isItSudoku(int matrix[][]) {
        return solve(matrix);
    }

    private static boolean solve(int[][] board) {

        for (int r = 0; r < 9; r++) {
            for (int c = 0; c < 9; c++) {

                if (board[r][c] == 0) {

                    for (int num = 1; num <= 9; num++) {

                        if (isSafe(board, r, c, num)) {
                            board[r][c] = num;

                            if (solve(board)) return true;

                            board[r][c] = 0; // backtrack
                        }
                    }
                    return false; // no valid number
                }
            }
        }
        return true; // solved
    }

    private static boolean isSafe(int[][] board, int r, int c, int num) {

        // Row check
        for (int i = 0; i < 9; i++)
            if (board[r][i] == num) return false;

        // Column check
        for (int i = 0; i < 9; i++)
            if (board[i][c] == num) return false;

        // 3x3 grid check
        int br = (r / 3) * 3;
        int bc = (c / 3) * 3;

        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++)
                if (board[br + i][bc + j] == num) return false;

        return true;
    }
}

```
