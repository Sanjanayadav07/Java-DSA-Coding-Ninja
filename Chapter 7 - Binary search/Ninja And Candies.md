# Minimum Days to Buy Candies 🧁

A Java program to calculate the **minimum number of days required** to buy all candies given daily sales, candy types, and required quantities.

---

## Problem Statement

Given:

- `days[]` → Days when candies are sold.  
- `candies[]` → Candy type sold on that day.  
- `k[]` → Number of candies required for each type.  
- `n` → Number of candy types.  
- `m` → Number of sales events.  

Goal: Find the **minimum number of days** needed to buy all candies such that leftover money can cover at least half of remaining candy requirements.

---
## Complexity

- Time Complexity: O(n * log(total_demand))
- Space Complexity: O(n + m + currDay)
---
## Features

- Calculates last sale day for each candy type.  
- Uses a greedy approach to allocate money.  
- Binary search to efficiently find the minimum day.  
- Handles large input sizes efficiently.

---

## Code

```java
import java.util.*;

public class Solution {

    static boolean isPossible(int[] days, int[] candies, int[] k, int n, int m, int currDay) {
        int[] lastSale = new int[n];
        Arrays.fill(lastSale, -1);

        for (int i = 0; i < m; i++) {
            if (days[i] <= currDay) {
                int candy = candies[i] - 1;
                lastSale[candy] = Math.max(lastSale[candy], days[i]);
            }
        }

        List<List<Integer>> saleOnDay = new ArrayList<>();
        for (int i = 0; i <= currDay; i++) saleOnDay.add(new ArrayList<>());

        for (int i = 0; i < n; i++) {
            if (lastSale[i] != -1) saleOnDay.get(lastSale[i]).add(i);
        }

        int[] need = k.clone();
        int money = 0;

        for (int day = 1; day <= currDay; day++) {
            money++;
            for (int candy : saleOnDay.get(day)) {
                if (money >= need[candy]) {
                    money -= need[candy];
                    need[candy] = 0;
                } else {
                    need[candy] -= money;
                    money = 0;
                    break;
                }
            }
        }

        int remaining = 0;
        for (int x : need) remaining += x;

        return remaining * 2 <= money;
    }

    static int[] toArray(ArrayList<Integer> list) {
        int[] arr = new int[list.size()];
        for (int i = 0; i < list.size(); i++) arr[i] = list.get(i);
        return arr;
    }

    public static int minimumDays(ArrayList<Integer> days,
                                  ArrayList<Integer> candies,
                                  ArrayList<Integer> k,
                                  int n, int m) {
        int total = 0;
        for (int x : k) total += x;

        int l = 0, h = total * 2, ans = 0;

        while (l <= h) {
            int mid = (l + h) / 2;

            if (isPossible(toArray(days), toArray(candies), toArray(k), n, m, mid)) {
                ans = mid;
                h = mid - 1;
            } else {
                l = mid + 1;
            }
        }
        return ans;
    }
}
```
