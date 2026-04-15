# 🏝️ Number of Islands II 

## 📌 Problem
Initially grid is all water 🌊  
Given queries → convert `(row, col)` to land 🌱  

👉 After each query, return **number of islands**

---

## 🧠 Key Idea

👉 After every land addition:
- Traverse full grid  
- Count islands using **DFS**

---

## 🛠️ Approach

### 🔹 Step 1: Add land

grid[row][col] = true


---

### 🔹 Step 2: Count islands

👉 For every cell:
- If land & not visited → DFS → island++

---

### 🔹 Step 3: DFS traversal

- Visit all 4 directions  
- Mark connected land  

---

## 💻 Code

```java
public class Solution {

    static int n, m;
    static int[][] dirs = {{-1,0},{1,0},{0,-1},{0,1}};

    public static void dfs(int row, int col, boolean[][] visited, boolean[][] grid) {

        if (row < 0 || row >= n || col < 0 || col >= m ||
            visited[row][col] || !grid[row][col]) {
            return;
        }

        visited[row][col] = true;

        for (int[] dir : dirs) {
            dfs(row + dir[0], col + dir[1], visited, grid);
        }
    }

    public static int[] numberOfIslandII(int rows, int cols, int[][] queries, int q) {

        n = rows;
        m = cols;

        int[] ans = new int[q];
        boolean[][] grid = new boolean[n][m];

        for (int k = 0; k < q; k++) {

            int row = queries[k][0];
            int col = queries[k][1];

            grid[row][col] = true;

            boolean[][] visited = new boolean[n][m];
            int count = 0;

            for (int i = 0; i < n; i++) {
                for (int j = 0; j < m; j++) {

                    if (grid[i][j] && !visited[i][j]) {
                        dfs(i, j, visited, grid);
                        count++;
                    }
                }
            }

            ans[k] = count;
        }

        return ans;
    }
}
```
---
### ⏱️ Time Complexity 
- O(Q * N * M)
- For each query → full grid traversal
- DFS inside → worst case N*M
### 📦 Space Complexity
- O(N * M)
