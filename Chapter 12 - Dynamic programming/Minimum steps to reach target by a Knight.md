## 📌 Problem Statement

- Given a chessboard of size N x N, a knight is placed at a starting position. You are given the target position.

- Return the minimum number of steps required for the knight to reach the target position.

- The knight moves in 8 possible L-shaped directions.

- If the target is unreachable, return 0.
---
## 💡 Approach
### 🔑 Key Idea:

- This is a Shortest Path in Unweighted Grid problem → solved using BFS (Breadth First Search).

- Since every move has equal cost (1 step), BFS guarantees the shortest path.
---
## 🪜 Steps:
- Treat the board as a graph
- Each cell = node
- Knight moves = edges (8 directions)
- Use BFS starting from the knight's position
- Maintain a visited[][] array to avoid revisiting nodes
- First time we reach target → return steps (guaranteed minimum)
---
## ♟️ Knight Moves:
```
(2,1), (2,-1), (-2,1), (-2,-1)
(1,2), (1,-2), (-1,2), (-1,-2)

```
---
## 🧾 Code
```
import java.util.*;

public class Solution {

    // Node class to store current position + steps
    static class Node {
        int steps, row, col;

        Node(int steps, int row, int col) {
            this.steps = steps;
            this.row = row;
            this.col = col;
        }
    }

    public static int minSteps(Pair knightPosition, Pair targetPosition, int size) {

        boolean[][] visited = new boolean[size + 1][size + 1];

        Queue<Node> queue = new LinkedList<>();

        queue.offer(new Node(0, knightPosition.second, knightPosition.first));

        visited[knightPosition.second][knightPosition.first] = true;

        int[] dr = {2, 2, 1, -1, -2, -2, -1, 1};
        int[] dc = {-1, 1, 2, 2, 1, -1, -2, -2};

        while (!queue.isEmpty()) {

            Node curr = queue.poll();

            if (curr.row == targetPosition.second &&
                curr.col == targetPosition.first) {
                return curr.steps;
            }

            for (int i = 0; i < 8; i++) {

                int newRow = curr.row + dr[i];
                int newCol = curr.col + dc[i];

                if (newRow > 0 && newCol > 0 &&
                    newRow <= size && newCol <= size &&
                    !visited[newRow][newCol]) {

                    visited[newRow][newCol] = true;
                    queue.offer(new Node(curr.steps + 1, newRow, newCol));
                }
            }
        }

        return 0;
    }
}
```
---
### ⏱️ Time Complexity
- O(N²)
- Each cell is visited at most once.

### 🧠 Space Complexity
- O(N²)
- For visited array + queue storage.
