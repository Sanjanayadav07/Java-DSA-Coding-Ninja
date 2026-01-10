# 🔄 Deque Implementation Using Array

## 📌 Problem Statement
Design and implement a **Deque (Double Ended Queue)** using an array.

A deque allows insertion and deletion from **both front and rear ends**.

---

## 🧠 Approach
- Use a **circular array** to efficiently utilize space
- Maintain two pointers:
  - `front` → points to the front element
  - `rear` → points to the rear element
- Handle circular movement using boundary checks
- Support operations:
  - `pushFront`
  - `pushRear`
  - `popFront`
  - `popRear`
  - `getFront`
  - `getRear`
  - `isEmpty`
  - `isFull`

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(1)` for all operations
- **Space Complexity:** `O(n)`

---

## 💻 Code

```java
import java.util.*;
import java.io.*;

public class Deque {

    int[] arr;
    int front;
    int rear;
    int size;

    // Initialize your data structure.
    public Deque(int n) {
        arr = new int[n];
        front = -1;
        rear = -1;
        size = n;
    }

    // Pushes 'x' in the front of the deque.
    public boolean pushFront(int x) {
        if (isFull()) return false;

        if (front == -1) {
            front = rear = 0;
        } else if (front == 0) {
            front = size - 1;
        } else {
            front--;
        }

        arr[front] = x;
        return true;
    }

    // Pushes 'x' in the back of the deque.
    public boolean pushRear(int x) {
        if (isFull()) return false;

        if (rear == -1) {
            front = rear = 0;
        } else if (rear == size - 1) {
            rear = 0;
        } else {
            rear++;
        }

        arr[rear] = x;
        return true;
    }

    // Pops element from front
    public int popFront() {
        if (isEmpty()) return -1;

        int val = arr[front];

        if (front == rear) {
            front = rear = -1;
        } else if (front == size - 1) {
            front = 0;
        } else {
            front++;
        }

        return val;
    }

    // Pops element from rear
    public int popRear() {
        if (isEmpty()) return -1;

        int val = arr[rear];

        if (front == rear) {
            front = rear = -1;
        } else if (rear == 0) {
            rear = size - 1;
        } else {
            rear--;
        }

        return val;
    }

    // Returns the first element
    public int getFront() {
        if (isEmpty()) return -1;
        return arr[front];
    }

    // Returns the last element
    public int getRear() {
        if (isEmpty()) return -1;
        return arr[rear];
    }

    // Checks if deque is empty
    public boolean isEmpty() {
        return front == -1;
    }

    // Checks if deque is full
    public boolean isFull() {
        return (front == 0 && rear == size - 1) || (front == rear + 1);
    }
}
