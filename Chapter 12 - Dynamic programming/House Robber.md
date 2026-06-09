# House Robber (Maximum Money Looted)

## 📌 Problem

A robber wants to rob houses arranged in a line.

Constraint:

Cannot rob two adjacent houses.

Find the maximum money that can be looted.

---

## 🧠 Key Idea

For every house we have only two choices:

1. Rob it
2. Skip it

Track both possibilities while traversing the array.

---

## 🔥 States

rob

Maximum money if current house is robbed.

noRob

Maximum money if current house is skipped.

---

## Transition

newRob =
noRob + houses[i]

newNoRob =
max(rob, noRob)

---

## Answer

max(rob, noRob)

---
## Code
```
import java.util.*;

public class Solution {
    public static int maxMoneyLooted(int[] houses) {
        //Your code goes here
        int rob = 0;
        int norob = 0;
        for(int i=0; i<houses.length; i++){
            int newrob = norob + houses[i];
            int newnorob = Math.max(norob, rob);
            rob = newrob;
            norob = newnorob;
        }

        return Math.max(rob, norob);

    }

}
```
---

## ⏱️ Complexity

Time Complexity:
O(N)

Space Complexity:
O(1)
