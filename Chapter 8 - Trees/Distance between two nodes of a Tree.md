# Distance Between Two Nodes in Binary Tree 🌳

This project provides a Java solution to find the **minimum distance between two given nodes** in a Binary Tree.

---

## 📌 Problem Statement

Given a binary tree and two node values `node1` and `node2`,  
find the **number of edges** in the shortest path between them.

If either node does not exist, return `-1`.

---

## 💡 Approach

The solution works in 3 steps:

### 1️⃣ Find Lowest Common Ancestor (LCA)
- If the current node is `null` or matches `node1` or `node2`, return it.
- Recursively search left and right.
- If both sides return non-null, current node is LCA.

### 2️⃣ Find Distance from LCA to Each Node
- Recursively calculate distance from LCA to `node1`.
- Recursively calculate distance from LCA to `node2`.

### 3️⃣ Return Total Distance
```
Distance = d1 + d2
```
---
## 🧠 Complexity Analysis
 - Time Complexity: O(N)
   - (Each node is visited at most once)
 - Space Complexity: O(H)
   - (Recursion stack, where H = height of the tree)
---

## 🚀 Code

```java
public class Solution
{
	public static TreeNode lca(TreeNode root,int a, int b) {
		if(root == null || root.val == a || root.val == b) {
			return root;
		}
		TreeNode left = lca(root.left,a,b);
		TreeNode right = lca(root.right,a,b);
		if(left == null) return right;
		if(right == null) return left;
		return root;
	}

	public static int distanceFromNode(TreeNode root,int key) {
		if(root == null) return -1;
		if(root.val == key) return 0;

		int left = distanceFromNode(root.left, key);
		if(left != -1) return left+1;

		int right = distanceFromNode(root.right, key);
		if(right != -1) return right+1;

		return -1;
	}

	public static int findDistanceBetweenNodes(TreeNode root, int node1, int node2)
	{
		TreeNode lca = lca(root, node1, node2);
		if(lca == null) return -1;

		int d1 = distanceFromNode(lca,node1);
		int d2 = distanceFromNode(lca,node2);

		return d1 + d2;
	}
}
