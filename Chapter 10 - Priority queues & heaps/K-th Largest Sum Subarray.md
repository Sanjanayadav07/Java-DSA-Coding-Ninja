# 🔺 Kth Largest Subarray Sum

## 📌 Problem
Given an array, find the **Kth largest subarray sum**.

👉 Subarray = continuous elements

---

## 🧠 Key Idea

- Generate **all subarray sums**
- Maintain only **K largest sums** using **Min Heap**

👉 Why Min Heap?
- Top element = **Kth largest**
- Keeps only top K elements efficiently

---

## 🛠️ Approach

### Step 1: Generate all subarrays


- for i → 0 to n-1
- for j → i to n-1
- sum += arr[j]

---

### Step 2: Maintain Min Heap of size K

- If heap size < K → add sum  
- Else:
  - If sum > heap.peek() → replace  


- if(size < k) add
- else if(sum > top) replace
---

## 💻  Code

```java
import java.util.*;

public class Solution {

    public static int getKthLargest(ArrayList<Integer> arr, int k) {

        int n = arr.size();

        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        for (int i = 0; i < n; i++) {

            int sum = 0;

            for (int j = i; j < n; j++) {

                sum += arr.get(j);

                if (minHeap.size() < k) {
                    minHeap.add(sum);
                } 
                else if (sum > minHeap.peek()) {
                    minHeap.poll();
                    minHeap.add(sum);
                }
            }
        }

        return minHeap.peek();
    }
}
```
---
### ⏱️ Time Complexity
- O(N^2 log K)
- Subarrays → O(N^2)
- Heap operations → log K
### 📦 Space Complexity
- O(K)
- Heap stores only K elements
