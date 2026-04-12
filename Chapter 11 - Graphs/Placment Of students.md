# 🤝 Placement of Student

## 📌 Problem
Given a binary matrix:
- Rows → Students (or left set)
- Columns → Jobs (or right set)

👉 `mat[i][j] = 1` means student `i` is eligible for job `j`

Find **maximum number of matches** such that:
- Each student gets at most 1 job
- Each job is assigned to at most 1 student

---

## 🧠 Key Idea

👉 This is a **Bipartite Matching problem**  
👉 Solve using **DFS + Augmenting Path**

---

## 🛠️ Approach

### 🔹 Step 1: Try assigning each student

For every student:
- Try to assign a job using DFS
- If job already taken → try to reassign previous student

---

### 🔹 Step 2: Matching array


- match[j] = i → job j is assigned to student i


---

### 🔹 Step 3: DFS logic

A job can be assigned if:
- It is free OR
- Previous student can be reassigned

---

## 💻 Code

```java
import java.util.*;

public class Solution {

    static boolean dfs(int i, int[][] mat, int[] match, boolean[] check, int n) {

        for (int j = 0; j < n; j++) {

            if (mat[i][j] == 1 && !check[j]) {

                check[j] = true;

                if (match[j] == -1 || dfs(match[j], mat, match, check, n)) {
                    match[j] = i;
                    return true;
                }
            }
        }

        return false;
    }

    public static int maxMatch(int[][] mat) {

        int m = mat.length;      // students
        int n = mat[0].length;   // jobs

        int[] match = new int[n];
        Arrays.fill(match, -1);

        int count = 0;

        for (int i = 0; i < m; i++) {

            boolean[] check = new boolean[n];

            if (dfs(i, mat, match, check, n)) {
                count++;
            }
        }

        return count;
    }
}
```
---
### ⏱️ Time Complexity
- O(N * M)
- Each student tries all jobs
- DFS may run multiple times
### 📦 Space Complexity
- O(N)
- match[] + visited array
