# 🌳 Height of Binary Tree from Inorder & Level Order
## 📌 Problem Statement
 - Given the Inorder and Level Order traversal of a binary tree.
 - Find the height of the tree.
 - Height = maximum number of edges from root to any leaf.
---
## 🧠 Approach
- Use Queue (BFS idea) to simulate tree construction.
- Store indices of inorder elements in a HashMap for quick lookup.
- Each queue node contains:
  - Current height
  - Left index range (in inorder)
  - Right index range (in inorder)
- Process elements in level order:
  - Find root position in inorder.
  - Split into left and right subtree ranges.
  - Push valid ranges into queue with updated height.
- Track maximum height during processing.

---
##⏱️ Complexity Analysis
 - Time Complexity: O(N)
 - Space Complexity: O(N)

---
## 💻 Code
```
import java.util.*;
import java.io.*;

class Node {
    int height;
    int leftIndex;
    int rightIndex;

    Node(int height, int leftIndex, int rightIndex) {
        this.height = height;
        this.leftIndex = leftIndex;
        this.rightIndex = rightIndex;
    }
}

public class Solution {

    public static int heightOfTheTree(int[] inorder, int[] levelOrder, int N) {

        Queue<Node> que = new LinkedList<>();
        Map<Integer, Integer> inorderMap = new HashMap<>();

        // Store inorder indices
        for (int i = 0; i < N; i++) {
            inorderMap.put(inorder[i], i);
        }

        // Root covers full inorder range
        que.add(new Node(0, 0, N - 1));
        int maxHeight = 0;

        for (int i = 0; i < N; i++) {

            int curr = levelOrder[i];
            Node now = que.poll();
            int currPos = inorderMap.get(curr);

            // Left subtree
            if (currPos > now.leftIndex) {
                Node leftNode = new Node(now.height + 1, now.leftIndex, currPos - 1);
                que.add(leftNode);
                maxHeight = Math.max(maxHeight, leftNode.height);
            }

            // Right subtree
            if (currPos < now.rightIndex) {
                Node rightNode = new Node(now.height + 1, currPos + 1, now.rightIndex);
                que.add(rightNode);
                maxHeight = Math.max(maxHeight, rightNode.height);
            }
        }

        return maxHeight;
    }
}
```
