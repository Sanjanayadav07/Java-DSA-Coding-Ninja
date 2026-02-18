# 🌳 Find Deepest Right Leaf Node 

This program finds the **deepest right leaf node** in a Binary Tree.

---

## 📌 Problem Statement

Given a Binary Tree, return the **deepest right leaf node**.

### A Right Leaf Node:
- It must be a **right child**
- It must have **no left and no right child**

If no right leaf exists, return a default node (e.g., `-1`).

---

## 🧠 Approach

We use **Level Order Traversal (BFS)**.

### Steps:
1. Use a `Queue` to perform BFS
2. Traverse nodes level by level
3. Whenever a right child is found:
   - Check if it is a leaf
   - If yes, update answer
4. The last valid right leaf found during BFS will be the deepest one

---
## ⏱️ Complexity Analysis
 - Time Complexity: O(n)
 - Space Complexity: O(n) (queue for BFS)

---

## 🧑‍💻 Code

```java
import java.util.*;

public class Solution {

	public static BinaryTreeNode<Integer> deepestRightLeaf(BinaryTreeNode<Integer> root) {

		if (root == null) return root;

		Queue<BinaryTreeNode<Integer>> q = new LinkedList<>();
		BinaryTreeNode<Integer> ans = new BinaryTreeNode<>(-1);

		q.offer(root);

		while (!q.isEmpty()) {

			BinaryTreeNode<Integer> curr = q.poll();

			if (curr.left != null)
				q.offer(curr.left);

			if (curr.right != null) {
				q.offer(curr.right);

				// Check if right child is a leaf
				if (curr.right.left == null && curr.right.right == null)
					ans = curr.right;
			}
		}

		return ans;
	}
}
