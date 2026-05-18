## 📌 Problem Statement

- Given an array arr of size n, determine whether it can be partitioned into two subsets with equal sum.

- Return:

  - true if possible
  - false otherwise
---
## 💡 Approach
### 🔑 Key Idea:

- If total sum is S, then we need to check:

- Can we find a subset with sum = S / 2 ?

- Because if one subset has sum S/2, the remaining automatically has S/2.
---
## 🪜 Steps:
- Compute total sum S
- If S is odd → return false
- Target = S / 2
- Use recursion + memoization (DP) to check subset sum
---
### 🧠 DP State
- t[i][x] = whether we can make sum x using elements from index i onward
- 🔁 Choices at each step:
- ✅ Take element:
    - if (nums[i] <= x)
    - take = solve(i + 1, x - nums[i])
- ❌ Don't take element:
  - not_take = solve(i + 1, x)
---
## 🧾 Code 
```
import java.util.*;

public class Solution {

    static int[][] t = new int[201][20001];

    static boolean solve(List<Integer> nums, int i, int x) {

        if (x == 0) return true;

        if (i >= nums.size()) return false;

        if (t[i][x] != -1) {
            return t[i][x] == 1;
        }

        boolean take = false;

        if (nums.get(i) <= x) {
            take = solve(nums, i + 1, x - nums.get(i));
        }

        boolean not_take = solve(nums, i + 1, x);

        t[i][x] = (take || not_take) ? 1 : 0;

        return take || not_take;
    }

    public static boolean canPartition(int[] arr, int n) {

        List<Integer> nums = new ArrayList<>();

        for (int num : arr) {
            nums.add(num);
        }

        int S = 0;

        for (int num : nums) {
            S += num;
        }

        if (S % 2 != 0) return false;

        for (int[] row : t) {
            Arrays.fill(row, -1);
        }

        return solve(nums, 0, S / 2);
    }
}
```
---
### ⏱️ Time Complexity
- O(n × sum/2)
- Each state (i, x) is computed once.

### 🧠 Space Complexity
- O(n × sum/2)
- For memoization table.
