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
The quickest sorting algorithm. Uses divide-and-conquer to sort. Doesn't produce
a stable sort.

### Algorithm
Select a pivot from the array (traditionally, first element). Reorder array so
that everything on left is smaller than the pivot, everything on the right is
greater than the pivot. Recursivley apply algorithim to smaller sublist and
greater sublist.

### Big O
Best case: O(N log N)
Avg case: O(N log N)

Worst case: O(N^2) - running on already sorted array

## Binary Search
![](https://upload.wikimedia.org/wikipedia/commons/8/83/Binary_Search_Depiction.svg)
Finds a specific element in a already sorted array. Works by comparing the target
element with the middle element in the array. If target element is less than
compared element, redo the process on the first half of the array. If target
element is more, then redo process on second half of the array. Stop when found
element or ran out of array.

### Big O
Best case: O(1) - first element compared matches!
Avg Case: O(log n)



## Graph

###  Breadth First Search
![](https://upload.wikimedia.org/wikipedia/commons/3/33/Breadth-first-tree.svg)

An algorithm for graph traversal. Starting at some node, visit all nodes at
current 'depth level' before going to the next depth level.

Good choice for finding the shortest distance between two nodes. Dijkstra's
Algorithm can be considered a modified BFS.

###  Depth First Search
![](https://upload.wikimedia.org/wikipedia/commons/1/1f/Depth-first-tree.svg)

An algorithm for graph traversal. Start at some node, explore down a single
'branch' as far as possible before backtracking.

Good choice for checking if graph is cyclic, and finding strongly connected
components of a graph (where every vertex is reachable from any other vertex)

### Kruskal's Algorithim (Minimum Spanning Tree)
Finds mimimum spanning tree. Smalles subset of edges (based on weight) that connects every vertex in graph.


#### Traversals

- Inorder Traversal: (Left, Root, Right)
- Preorder Traversal: (Root, Left, Right)
- Postorder Traversal: (Left, Right, Root)



# Data Structures
## List

### Linked List
Data structure where each element has pointer to the next element (single linked list)
and optionally a pointer to the last element (double linked list)

O(N) for accessing certain positon in list. O(1) add and remove,

## Trees
A tree is a directed acyclic graph
### Binary Tree
A specific tree where each node has at most 2 children

### Binary Search Tree
A specific binary tree where every node's left child is less than the node, and
every node's right child is more than the node. 

Has avg O(log N) search, insert, delete operations. 




## Stack
Last in, first out data structure. Adding elements add it to the top of the
stack, popping takes the top element from the stack.

Useful for backtracking in graph theory. Example: Using depth first search, we
add the nodes we're visiting to the stack. When we reach the final node of a
branch, we pop the stack to 'backtrack' to the last branching point.

## Queue
First in, first out data structure. Adding elements adds it to the top of the
queue, popping an element takes the bottom element.


