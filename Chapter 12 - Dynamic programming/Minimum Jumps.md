## 📌 Problem Statement

- Given an array arr[] of size N, where each element represents the maximum number of steps you can jump forward from that index, find the minimum number of jumps required to reach the last index.

- If reaching the end is not possible, return -1.
---
## 💡 Approach (Greedy)

- This problem is solved using a Greedy approach.

## 🧠 Key Idea:
- At every index, track the farthest position (max) you can reach.
- Maintain a range (choice) which represents the current jump boundary.
- When you reach the end of the current range (i == choice), you must take a jump.
---
## ⚙️ Steps:
- Initialize:
   - max → farthest reachable index
   - choice → end of current jump range
   - jumps → number of jumps
- Traverse the array:
    - Update max = max(max, arr[i] + i)
- If i == choice, it means:
    - You must take a jump
    - Update choice = max
    - Increment jumps
- After traversal:
    - If choice >= N-1 → return jumps
    - Else → return -1
---
## Code 
```
public class Solution {

    public static int minimumJumps(int[] arr, int N) {
        N = arr.length;

        int max = 0;      // Farthest index reachable
        int choice = 0;   // Current jump boundary
        int jumps = 0;    // Number of jumps

        for (int i = 0; i < N - 1; i++) {

            // Update farthest reachable index
            max = Math.max(max, arr[i] + i);

            // If we reach the end of current jump range
            if (i == choice) {
                choice = max;
                jumps++;
            }
        }

        // Check if last index is reachable
        if (choice >= N - 1) {
            return jumps;
        } else {
            return -1;
        }
    }
}
```
---
### ⏱️ Time Complexity
- O(N)
- Single traversal of the array
  
### 💾 Space Complexity
- O(1)
- No extra space used (only variables)
