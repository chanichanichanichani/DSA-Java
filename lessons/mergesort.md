---
path: "/mergesort"
title: "Merge Sort"
order: "8E"
section: "Recursion"
description: "learn Recursion from scratch"
---
# Merge Sort

## 1. Introduction
Merge Sort is a **Divide & Conquer** sorting algorithm.  
The main idea: split the array into two halves, sort each half recursively, and then **merge** the two sorted halves into one sorted array.  
It is stable, always runs in **O(n log n)** time, but requires **O(n)** extra space.

---

## 2. Understanding the Merge Sort
1. If the array has length 0 or 1 → already sorted.  
2. Split the array into two halves.  
3. Sort each half using Merge Sort (recursive calls).  
4. Merge the two halves into a single sorted array.  

---

## 3. Implementation + Illustration
Example walkthrough with array `[5, 2, 4, 6, 1, 3]`:

Step 1: Split → [5, 2, 4] | [6, 1, 3]  
Step 2: Split → [5] [2,4] | [6] [1,3]  
Step 3: Split → [5] [2] [4] | [6] [1] [3]  
Step 4: Merge → [2,4,5] | [1,3,6]  
Step 5: Merge → [1,2,3,4,5,6]

---

## 4. Code for Merge Sort (Java)

```java
public class MergeSort {
    public static void sort(int[] arr) {
        if (arr.length <= 1) return;
        mergeSort(arr, 0, arr.length - 1);
    }

    private static void mergeSort(int[] arr, int left, int right) {
        if (left >= right) return;
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }

    private static void merge(int[] arr, int left, int mid, int right) {
        int[] temp = new int[right - left + 1];
        int i = left, j = mid + 1, k = 0;

        while (i <= mid && j <= right) {
            if (arr[i] <= arr[j]) temp[k++] = arr[i++];
            else temp[k++] = arr[j++];
        }
        while (i <= mid) temp[k++] = arr[i++];
        while (j <= right) temp[k++] = arr[j++];

        for (i = left; i <= right; i++) arr[i] = temp[i - left];
    }

    public static void main(String[] args) {
        int[] arr = {5, 2, 4, 6, 1, 3};
        sort(arr);
        for (int x : arr) System.out.print(x + " ");
        // Output: 1 2 3 4 5 6
    }
}
