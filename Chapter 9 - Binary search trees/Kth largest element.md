# 🏆 Kth Largest Element in an Array

## 📌 Problem Statement
Given an array of integers `nums` and an integer `k`, return the **kth largest element** in the array.

The kth largest element is the element that appears in position `k` if the array is sorted in **descending order**.

### ✨ Example
```
Input:
nums = [3,2,1,5,6,4]
k = 2

Output:
5
```

📖 **Explanation:**  
Sorted array (descending) → `[6,5,4,3,2,1]`  
The **2nd largest element is 5**.

---

# 💡 Approach (Min Heap)

We use a **Min Heap (PriorityQueue)** to keep track of the `k` largest elements.

### 🚀 Steps
1️⃣ Create a **Min Heap** using `PriorityQueue`.  
2️⃣ Traverse each element of the array.  
3️⃣ Insert the element into the heap.  
4️⃣ If heap size becomes greater than `k`, remove the smallest element using `poll()`.  
5️⃣ After processing all elements, the top of the heap (`peek()`) will be the **kth largest element**.

📌 The heap always maintains the **k largest elements** seen so far.

---

# 💻  Code

```java
import java.util.*;

public class Solution {
    public static int findKthLargest(ArrayList<Integer> nums, int k) {

        // 🧠 Min Heap
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        // 🔁 Traverse elements
        for (int num : nums) {
            pq.add(num);

            // 📏 Maintain heap size k
            if (pq.size() > k) {
                pq.poll();
            }
        }

        // 🎯 kth largest element
        return pq.peek();
    }
}
```

---

# ⏱ Time Complexity

```
O(n log k)
```

📌 Insertion into heap takes `O(log k)`  
📌 Done for `n` elements

---

# 🧠 Space Complexity

```
O(k)
```

The heap stores at most **k elements**.

---

# ✅ Key Idea

Instead of sorting the entire array (`O(n log n)`), we maintain a **heap of size k** which improves efficiency when `k` is small.

---

⭐ If you found this helpful, consider giving the repository a **star**!
