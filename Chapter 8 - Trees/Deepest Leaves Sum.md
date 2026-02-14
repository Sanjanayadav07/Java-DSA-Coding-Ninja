# Deepest Leaves Sum
## 🟢 Problem Statement
 - Given the root of a binary tree, return the sum of values of its deepest leaves.
 - A leaf is a node with no children.
 - The deepest leaves are the leaf nodes located at the maximum depth of the tree.
 - If the tree is empty (root == null), return 0.

## 🟢 Approach (Level Order Traversal – BFS)
  - We use Breadth-First Search (BFS) to traverse the tree level by level.
  - Why BFS?
  - Because BFS naturally processes nodes level by level, and the last processed level will be the deepest level.
  - Steps:
     - If root is null, return 0.
     - Use a Queue to perform level order traversal.
 - Traverse the tree level by level:
 - For each level:
    - Reset sum = 0
    - Add all node values of that level
    - Add their children to the queue
    - When traversal finishes, sum will contain the sum of the deepest level.
 - Return sum.

## 🟢 Time and Space Complexity
 - Time Complexity: O(N)
   - (Every node is visited once)
 - Space Complexity: O(N)
   - (Queue may contain all nodes of a level)

## 🟢 Code 
```
import java.util.*;

public class Solution {
    public static int deepestLeavesSum(TreeNode root) {
        if (root == null) return 0;

        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        int sum = 0;

        while (!q.isEmpty()) {
            int size = q.size();
            sum = 0;  // Reset sum for each level

            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                sum += node.val;

                if (node.left != null) q.offer(node.left);
                if (node.right != null) q.offer(node.right);
            }
        }
        return sum;
    }
}
```
