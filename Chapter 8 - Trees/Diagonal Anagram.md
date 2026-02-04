# 🌲 Diagonal Anagram Check in Binary Trees 

## 📌 Problem Statement
Given two binary trees, determine whether they are **diagonal anagrams** of each other.

Two trees are said to be diagonal anagrams if:
- For every diagonal, the set of node values in both trees is the same (order does not matter).

---

## 🧠 Approach
- Use **diagonal traversal** for both trees
- Maintain **two queues** to process diagonals level by level
- For each diagonal:
  - Traverse using right pointers
  - Push left children into the queue for the next diagonal
- Store diagonal elements in lists
- **Sort and compare** the lists to check anagram property
- If all diagonals match → return `true`

---
## ⏱️ Complexity Analysis
  - Time Complexity: O(N log N)
  - Space Complexity: O(N)
---

## 💻 Code

```java
import java.util.*;

public class Solution {

    public static boolean diagonalAnagram(BinaryTreeNode<Integer> root1,
                                           BinaryTreeNode<Integer> root2) {

        if (root1 == null && root2 == null) return true;
        if (root1 == null || root2 == null) return false;

        Queue<BinaryTreeNode<Integer>> q1 = new LinkedList<>();
        Queue<BinaryTreeNode<Integer>> q2 = new LinkedList<>();

        q1.add(root1);
        q2.add(root2);

        while (!q1.isEmpty() && !q2.isEmpty()) {

            int size1 = q1.size();
            int size2 = q2.size();

            if (size1 != size2) return false;

            ArrayList<Integer> d1 = new ArrayList<>();
            ArrayList<Integer> d2 = new ArrayList<>();

            // Process one diagonal
            for (int i = 0; i < size1; i++) {

                BinaryTreeNode<Integer> t1 = q1.poll();
                BinaryTreeNode<Integer> t2 = q2.poll();

                while (t1 != null) {
                    d1.add(t1.data);
                    if (t1.left != null) q1.add(t1.left);
                    t1 = t1.right;
                }

                while (t2 != null) {
                    d2.add(t2.data);
                    if (t2.left != null) q2.add(t2.left);
                    t2 = t2.right;
                }
            }

            Collections.sort(d1);
            Collections.sort(d2);

            if (!d1.equals(d2)) return false;
        }

        return q1.isEmpty() && q2.isEmpty();
    }
}
