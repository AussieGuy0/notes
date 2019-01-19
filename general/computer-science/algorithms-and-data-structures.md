# Algorithms & Data Structures

# Sorting

## Insertion Sort

![](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)

### Description
A simple sorting algorithm that sorts one element at a time, building a sorted list in place at the start of the array. 

### Algorithm
Start at the second element of array.

Compare to each element in the 'sorted list', if current element is smaller then 
sorted element, swap it! Continue comparing until a current element is larger 
than sorted element, or you run out of sorted elements (current element is smallest element)

Go to next element in unsorted list and repeat the process until completely sorted!

### Big O
Best Case: O(N) - When array is already sorted

Avg Case: O(N^2)

## Selection Sort
### Description
Extremely simple algorithm that sorts one element at a time, building a sorted list in place at the start of the array

### Algorithm
Find the smallest element in unsorted list, put at end of sorted list. The sort
finishes when our sorted list has the length on n-1.

### Big O
Best Case: O(N^2)

Avg Case: O(N^2)

## Bubble Sort
### Description
Simple algorithm that compares two elements at a time, swapping them if the right 
element is smaller than the left element. Complete garbage and shouldn't be used
in the real world.

### Algorithm
Compare first two elements in array, if right element small than left element
swap. Increase index positons by one and repeat. If no elements were swapped in
a full loop, the list is sorted.

### Big O
Best case: O(N) - When array is already sorted

Avg Case: O(N^2)

## Merge Sort
![](https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif)
### Description
Efficent, recursive algorthim which produces a stable sort (order of
equal elements the same)

### Algorithm
Divide the array into N sublists, each containing one element. Then, repeatly
merge sublists into sorted sublists untill one sublist (the sorted array)
remains.

### Big O
Best case: O(N log N)

Avg Case: O(N log N)


## Quick Sort
### Description

### Algorithm

### Big O
Best case: O(N log N)

Avg case: O(N log n)

Worst case: O(N^2) - running on already sorted array

# Search

## Binary Search

## Tree

- Inorder Traversal
- Preorder Traversal
- Postorder Traversal
- Kruskal's Algorithim (Minimum Spanning Tree)

## Graph

- Breadth First Search
- Depth First Search

# Data Structures

## List

- Linked List

## Binary Tree

- Binary Search Tree

## Stack

## Queue

## Graph

## Tree
