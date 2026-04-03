## Problem Statement

- You are given an array of integers stones where stones[i] represents the weight of the i-th stone.
- Each turn, you select the two heaviest stones and smash them together:

- If the weights are equal, both stones are destroyed.
- If the weights are unequal, the lighter stone is destroyed, and the heavier stone's weight is reduced by the lighter stone's weight.

- Return the weight of the last remaining stone. If no stones remain, return 0.

---
## Approach
- Use a Max-Heap (PriorityQueue with reverse order) to always pick the two largest stones.
- Repeat the process until 0 or 1 stone remains:
- Poll the two largest stones.
- If they are different, insert the difference back into the heap.
- Return the last stone’s weight or 0 if the heap is empty.

---
### Time Complexity: 
- O(n log n) – inserting and removing from heap is log n, done n times
### Space Complexity: 
- O(n) – for the heap

---
## Code
```
import java.util.PriorityQueue;
import java.util.Collections;

public class Solution {
    public static int weightOfLastStone(int arr[]) {

        // Max-Heap
        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());

        // Insert all elements into heap
        for (int stone : arr) {
            pq.add(stone);
        }

        // Smash stones
        while (pq.size() > 1) {
            int a = pq.poll();  // largest
            int b = pq.poll();  // second largest

            if (a != b) {
                pq.add(Math.abs(a - b));
            }
        }

        // Return remaining stone or 0
        return pq.isEmpty() ? 0 : pq.peek();
    }
}
```
----
