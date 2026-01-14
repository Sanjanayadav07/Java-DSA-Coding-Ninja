# 👑 N-Queens Problem (Backtracking)

## 📌 Problem Statement
Given an integer `n`, place `n` queens on an `n × n` chessboard such that:

- No two queens attack each other
- Queens cannot share the same **row**, **column**, or **diagonal**

Return **all possible valid board configurations**.

---

## 🧠 Approach (Backtracking)
We place **one queen per row** and try all possible columns:

1. Start from row `0`
2. For each column:
   - Check if placing a queen is **safe**
3. If safe:
   - Place the queen
   - Recur for the next row
4. If all rows are filled → store solution
5. Backtrack and try other possibilities

---

## 🔍 Safety Check Conditions
For a queen at `(row, col)`:
- ❌ Same column → `queens[i] == col`
- ❌ Same diagonal → `|row - i| == |col - queens[i]|`

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(N!)`
- **Space Complexity:** `O(N)` (recursion + board storage)

---

## 💻 Code

```java
import java.util.*;
import java.io.*;

public class Solution {

    static ArrayList<int[]> boards;

    public static ArrayList<ArrayList<Integer>> nQueens(int n) {

        boards = new ArrayList<>();
        int[] queens = new int[n];
        solve(0, queens, n);

        // Convert to required output format
        ArrayList<ArrayList<Integer>> res = new ArrayList<>();

        for (int[] q : boards) {
            ArrayList<Integer> board = new ArrayList<>();
            for (int r = 0; r < n; r++) {
                for (int c = 0; c < n; c++) {
                    if (q[r] == c) board.add(1);
                    else board.add(0);
                }
            }
            res.add(board);
        }

        return res;
    }

    private static void solve(int row, int[] queens, int n) {

        if (row == n) {
            boards.add(queens.clone());
            return;
        }

        for (int col = 0; col < n; col++) {
            if (isValid(queens, row, col)) {
                queens[row] = col;
                solve(row + 1, queens, n);
            }
        }
    }

    private static boolean isValid(int[] queens, int row, int col) {

        for (int i = 0; i < row; i++) {
            int qCol = queens[i];

            // Same column
            if (qCol == col) return false;

            // Same diagonal
            if (Math.abs(i - row) == Math.abs(qCol - col)) return false;
        }
        return true;
    }
}
