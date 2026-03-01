# 🌳 Merge Two BSTs

This problem merges two **Binary Search Trees (BSTs)**  
into a single **sorted list**.

---

## 🧠 Approach Used
- 🔹 Step 1: Inorder Traversal
   - Inorder of BST gives sorted order
   - Store elements of both BSTs separately

- 🔹 Step 2: Merge Two Sorted Lists
   - Use two pointers (i, j)
   - Compare elements and add smaller one
   - Append remaining elements at the end

---
## ⏱️ Complexity:
- Time Complexity: O(N + M)
- Space Complexity: O(N + M)

---

## 💻 Code

```java
import java.util.*;

public class Solution {

    // Main function to merge two BSTs
    public static List<Integer> mergeBST(TreeNode root1, TreeNode root2) {
        List<Integer> list1 = new ArrayList<>();
        List<Integer> list2 = new ArrayList<>();

        // Step 1: Inorder traversal of both BSTs
        inorder(root1, list1);
        inorder(root2, list2);

        // Step 2: Merge the two sorted lists
        return mergeSortedLists(list1, list2);
    }

    // Iterative Inorder Traversal (Left → Root → Right)
    private static void inorder(TreeNode root, List<Integer> list) {
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;

        while (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.push(curr);
                curr = curr.left;
            }

            curr = stack.pop();
            list.add(curr.data);
            curr = curr.right;
        }
    }

    // Merge two sorted lists in O(N) time
    private static List<Integer> mergeSortedLists(List<Integer> list1, List<Integer> list2) {
        List<Integer> merged = new ArrayList<>();
        int i = 0, j = 0;

        while (i < list1.size() && j < list2.size()) {
            if (list1.get(i) <= list2.get(j)) {
                merged.add(list1.get(i++));
            } else {
                merged.add(list2.get(j++));
            }
        }

        while (i < list1.size()) merged.add(list1.get(i++));
        while (j < list2.size()) merged.add(list2.get(j++));

        return merged;
    }
}
