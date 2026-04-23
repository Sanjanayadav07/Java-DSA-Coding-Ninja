# 🐍 Snakes and Ladders (Minimum Dice Throws - BFS)
## 📌 Problem
- Given a board:
- You start from cell 1
- Goal is to reach n*n
- You can roll dice (1 to 6)
- Some cells have:
- 🐍 Snake → moves you down
- 🪜 Ladder → moves you up

- 👉 Find minimum dice throws required to reach last cell
---
## 🧠 Key Idea
- 👉 Treat board as a graph problem

- ✔ Each cell = node
- ✔ Dice (1–6) = edges
- ✔ Snake/Ladder = direct jump

- 👉 Use BFS to find shortest path

##  ⚡ Why BFS?

- 👉 Because:

- Each dice move = equal cost (1 step)
- BFS guarantees minimum moves
- First time reaching destination = shortest path
---
## 🛠️ Approach
### 🔹 Step 1: Model the Board
- Convert 1D cell → 2D matrix (zigzag pattern)
### 🔹 Step 2: BFS Initialization
- Start from cell 1
- Use queue
- Mark visited
### 🔹 Step 3: Explore Moves
- For each cell:
- Try dice values (1 to 6)
- Move to next cell
- Apply snake/ladder jump
### 🔹 Step 4: Level Tracking
- Each BFS level = 1 dice throw
- Increase steps after each level
### 🔹 Step 5: Stop Condition
- If reached n*n → return steps
---
## 💻  Code
```
import java.util.*;

public class Solution {

    static int n;

    // Convert cell number to board coordinates (zigzag pattern)
    private static int[] getCoord(int s) {
        int row = n - 1 - (s - 1) / n;
        int col = (s - 1) % n;

        if ((n % 2 == 1 && row % 2 == 1) || (n % 2 == 0 && row % 2 == 0)) {
            col = n - 1 - col;
        }

        return new int[]{row, col};
    }

    public static int minDiceThrowToLastCell(int[][] board) {
        n = board.length;

        boolean[] visited = new boolean[n * n + 1];

        Queue<Integer> queue = new LinkedList<>();
        queue.offer(1);
        visited[1] = true;

        int steps = 0;

        while (!queue.isEmpty()) {

            int size = queue.size();

            while (size-- > 0) {

                int curr = queue.poll();

                if (curr == n * n) return steps;

                for (int dice = 1; dice <= 6; dice++) {

                    int next = curr + dice;
                    if (next > n * n) break;

                    int[] coord = getCoord(next);
                    int r = coord[0];
                    int c = coord[1];

                    // snake or ladder
                    if (board[r][c] != -1) {
                        next = board[r][c];
                    }

                    if (!visited[next]) {
                        visited[next] = true;
                        queue.offer(next);
                    }
                }
            }

            steps++;
        }

        return -1;
    }
}
```
----
### ⏱️ Time Complexity
- O(n^2)
- Each cell visited once

### 📦 Space Complexity
- O(n^2)
- Queue + visited array
