# Graph Coloring Problem

## 📌 Problem
Assign colors to graph nodes such that no two adjacent nodes have same color.

Return "YES" if possible using at most m colors, else "NO".

---

## 🧠 Approach
- Use Backtracking
- Try each color for every node
- Check adjacency constraint
- Backtrack if conflict occurs

---
## Code 
```
// Graph Coloring using Backtracking
// Time Complexity: O(m^n)
// Space Complexity: O(n)

public class Solution {

    public static String graphColoring(int[][] mat, int m) {

        int n = mat.length;
        int[] color = new int[n]; // store color of each node

        if (solve(mat, color, m, 0)) {
            return "YES";
        }
        return "NO";
    }

    // Backtracking function
    private static boolean solve(int[][] mat, int[] color, int m, int node) {

        // all nodes colored successfully
        if (node == mat.length) return true;

        // try all colors
        for (int c = 1; c <= m; c++) {

            if (isSafe(mat, color, node, c)) {

                color[node] = c;

                if (solve(mat, color, m, node + 1)) {
                    return true;
                }

                color[node] = 0; // backtrack
            }
        }

        return false;
    }

    // Check if color can be assigned
    private static boolean isSafe(int[][] mat, int[] color, int node, int c) {

        for (int i = 0; i < mat.length; i++) {

            // adjacent node has same color
            if (mat[node][i] == 1 && color[i] == c) {
                return false;
            }
        }

        return true;
    }
}
```
---

## ⚡ Complexity
- Time: O(m^n)
- Space: O(n)
