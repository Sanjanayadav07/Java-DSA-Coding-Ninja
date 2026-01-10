# 🗼 Tower of Hanoi (Recursive) 

## 📌 Problem Statement
You are given `n` disks placed on **Rod 1**.

Your task is to move all the disks to **Rod 3** using **Rod 2** as an auxiliary rod, following these rules:
- Only one disk can be moved at a time
- A larger disk cannot be placed on top of a smaller disk
- Each move is represented as a pair `[from, to]`

Return all the moves required to solve the problem.

---

## 🧠 Approach (Recursion)
The problem follows a classic recursive pattern:

1. Move `n-1` disks from **source → auxiliary**
2. Move the nth disk from **source → destination**
3. Move `n-1` disks from **auxiliary → destination**

Each move is stored as a pair `[source, destination]`.

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(2^n)`
- **Space Complexity:** `O(2^n)` (to store moves + recursion stack)

---

## 💻 Code

```java
import java.util.ArrayList;

public class Solution {

    public static ArrayList<ArrayList<Integer>> towerOfHanoi(int n) {

        ArrayList<ArrayList<Integer>> ans = new ArrayList<>();

        int src = 1, aux = 2, dest = 3;

        solverRec(n, ans, src, aux, dest);

        return ans;
    }

    private static void solverRec(int n, ArrayList<ArrayList<Integer>> ans,
                                  int src, int aux, int dest) {

        if (n == 0) return;

        solverRec(n - 1, ans, src, dest, aux);

        ArrayList<Integer> move = new ArrayList<>();
        move.add(src);
        move.add(dest);
        ans.add(move);

        solverRec(n - 1, ans, aux, src, dest);
    }
}
