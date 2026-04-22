# 🍊 Rotten Oranges (Multi-Source BFS)

## 📌 Problem
Given a grid:
- `0` → empty  
- `1` → fresh orange 🍊  
- `2` → rotten orange 🤢  

- 👉 Every minute, rotten oranges infect adjacent fresh ones  

- 👉 Find **minimum time to rot all oranges**

---

## 🧠 Key Idea

👉 Use **Multi-Source BFS**

✔ Start BFS from **all rotten oranges simultaneously**  
✔ Spread infection level by level (minute by minute)

---

## ⚡ Why Multi-Source BFS?

- 👉 Because multiple rotten oranges spread at the same time  
- All rotten nodes = starting points
---

## 🛠️ Approach

### 🔹 Step 1: Initialization

- Add all rotten oranges to queue  
- Count fresh oranges  

---

### 🔹 Step 2: BFS Traversal

- Process level by level  
- Each level = 1 minute  

---

### 🔹 Step 3: Rot Adjacent

- Check 4 directions  
- Convert fresh → rotten  
- Decrease fresh count  

---

### 🔹 Step 4: Final Check


- If freshCount == 0 → return time
- Else → return -1
---

## 💻 Code

```java
import java.util.*;

public class Solution {

    public static int minTimeToRot(int[][] grid, int n, int m) {
        
        Queue<int[]> queue = new LinkedList<>();
        int freshCount = 0;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (grid[i][j] == 2) {
                    queue.offer(new int[]{i, j});
                } else if (grid[i][j] == 1) {
                    freshCount++;
                }
            }
        }

        if (freshCount == 0) return 0;

        int[][] directions = {
            {-1, 0}, {1, 0}, {0, -1}, {0, 1}
        };

        int time = 0;

        while (!queue.isEmpty()) {
            int size = queue.size();
            boolean rotted = false;

            while (size-- > 0) {
                int[] curr = queue.poll();
                int x = curr[0];
                int y = curr[1];

                for (int[] dir : directions) {
                    int nx = x + dir[0];
                    int ny = y + dir[1];

                    if (nx >= 0 && nx < n && ny >= 0 && ny < m && grid[nx][ny] == 1) {
                        grid[nx][ny] = 2;
                        queue.offer(new int[]{nx, ny});
                        freshCount--;
                        rotted = true;
                    }
                }
            }

            if (rotted) time++;
        }

        return freshCount == 0 ? time : -1;
    }
}
```
---
### ⏱️ Time Complexity
- O(N * M)
- Each cell visited once
### 📦 Space Complexity
- O(N * M)
- Queue in worst case
