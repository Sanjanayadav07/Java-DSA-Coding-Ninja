# Partition Array Into K Equal Sum Subsets

## 📌 Problem
Divide array into K subsets such that:
- Every subset has equal sum

Return true if possible.

---

## 🧠 Approach
Use Backtracking:

- Build one subset at a time
- Mark used elements
- Once subset sum reaches target:
    move to next subset

---

## 🔥 Key Observation
Total sum must be divisible by K.

target = totalSum / K

---

## Code
```
import java.util.*;

public class Solution {

    static boolean back(int[] nums, int i, int k, int target, int sum) {

        // All subsets formed
        if (k == 0) {
            return true;
        }

        // One subset completed
        if (sum == target) {
            return back(nums, 0, k - 1, target, 0);
        }

        // Out of bounds
        if (i >= nums.length) {
            return false;
        }

        // Take current element
        if (nums[i] != -1 && sum + nums[i] <= target) {

            int val = nums[i];
            nums[i] = -1;

            if (back(nums, i + 1, k, target, sum + val)) {
                return true;
            }

            nums[i] = val;

            // Not take current element
            if (back(nums, i + 1, k, target, sum)) {
                return true;
            }

            return false;
        }

        // Skip current element
        return back(nums, i + 1, k, target, sum);
    }

    public static boolean canPartitionKSubsets(int[] nums, int n, int k) {

        int sum = 0;

        for (int num : nums) {
            sum += num;
        }

        // Sum must be divisible by k
        if (sum % k != 0) {
            return false;
        }

        int target = sum / k;

        return back(nums, 0, k, target, 0);
    }
}
```
---

## ⚡ Complexity
- Time: Exponential
- Space: O(N)
