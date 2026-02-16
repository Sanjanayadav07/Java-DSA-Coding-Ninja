# 🌳 Form Largest Number from Binary Tree 

This program forms the **largest possible number** using the values of all nodes in a Binary Tree.

---

## 📌 Problem Statement

Given a Binary Tree:
- Collect all node values
- Arrange them in such an order that they form the **largest possible number**
- Return the number as a `String`

---

## 🧠 Approach

### Step 1️⃣: Traverse the Tree
- Use **DFS (Preorder Traversal)**
- Store all node values as strings in a list

### Step 2️⃣: Custom Sorting
Sort using comparator:
```
(s2 + s1).compareTo(s1 + s2)

```

This ensures:
- Larger concatenation comes first
- Example:
  - "9" + "34" = "934"
  - "34" + "9" = "349"
  - Since 934 > 349 → "9" should come before "34"

### Step 3️⃣: Build Final Number
- Append all sorted strings
- Edge case: If first digit is '0', return "0"

---
## ⏱️ Complexity Analysis
  - Total Time Complexity: O(n log n)
  - Space Complexity: O(n)
    
---
## 🧑‍💻 Code

```java
import java.util.*;

public class Solution {

    private static void dfs(BinaryTreeNode<Integer> root, List<String> nodes) {
        if (root == null) return;

        nodes.add(String.valueOf(root.data));
        dfs(root.left, nodes);
        dfs(root.right, nodes);
    }

    public static String printLargest(BinaryTreeNode<Integer> root) {

        List<String> nodes = new ArrayList<>();

        dfs(root, nodes);

        Collections.sort(nodes, (s1, s2) -> (s2 + s1).compareTo(s1 + s2));

        StringBuilder number = new StringBuilder();

        for (String num : nodes) {
            number.append(num);
        }

        // Edge case: if all numbers are 0
        if (number.length() > 0 && number.charAt(0) == '0') {
            return "0";
        }

        return number.toString();
    }
}

