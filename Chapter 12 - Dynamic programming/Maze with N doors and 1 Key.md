# Problem Statement

You are given an `N × N` maze where:

- `0` represents an empty cell (no door)
- `1` represents a locked door

You start from the top-left cell `(0,0)` and need to reach the bottom-right cell `(N-1,N-1)`.

You can move only:
- Right
- Down

You have only **one key**, which means you can pass through **at most one locked door**.

Return `true` if it is possible to reach the destination, otherwise return `false`.

---

# Approach

## Key Idea

Instead of checking every possible path, we calculate the minimum number of doors encountered on any path from the start to the destination.

Let:

f(i, j) = Minimum number of doors crossed from cell `(i, j)` to `(N-1, N-1)`.

At each cell, we can either move:

1. Down
2. Right

So we choose the path requiring fewer doors.

---

## Recurrence

If we are at cell `(i, j)`:

f(i, j) = maze[i][j] + min(f(i+1, j), f(i, j+1))

---

## Base Cases

### Out of Bounds

If:

i >= n OR j >= n

Return 2 (a large enough value since we only care whether answer is ≤ 1).

### Destination Reached

If:

i == n-1 && j == n-1

Return maze[i][j].

---

# Code

```java
import java.util.* ;
import java.io.*; 

public class Solution {

    static int[][] dp = new int[101][101];

    static int f(int i, int j, int n, ArrayList<ArrayList<Integer>> maze) {
        if (i >= n || j >= n) {
            return 2;
        }

        if (i == n - 1 && j == n - 1) {
            return maze.get(i).get(j);
        }

        if (dp[i][j] != -1) {
            return dp[i][j];
        }

        dp[i][j] = maze.get(i).get(j)
                + Math.min(
                    f(i + 1, j, n, maze),
                    f(i, j + 1, n, maze)
                );

        return dp[i][j];
    }

    public static boolean mazeWithNDoorsAnd1Key(ArrayList<ArrayList<Integer>> maze, int n) {
        for (int i = 0; i < 101; i++) {
            Arrays.fill(dp[i], -1);
        }

        return f(0, 0, n, maze) <= 1;
    }
}
