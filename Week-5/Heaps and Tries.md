# Heaps 

A Heap is a complete binary tree data structure that satisfies the heap property: for every node, the value of its children is greater than or equal to its own value. Heaps are usually used to implement priority queues, where the smallest (or largest) element is always at the root of the tree.

## Priority queue
A priority queue is a type of data structure where each element has a priority assigned to it. Elements are processed based on their priority, with higher priority elements being processed before lower priority ones. This is different from a regular queue where elements are processed in the order they arrive (first-in, first-out).

### Example
```cpp
#include <iostream>
#include <queue>
using namespace std;

int main() {
    
    // Creating a priority queue of integers
    priority_queue<int> pq;
    pq.push(9);
    pq.push(10);
    pq.push(6);
    
    cout << pq.top() << " ";
    return 0;
}
```
### Output
```
10
```
In the above program, we created a priority queue of integers that contains the elements 9, 10 and 6. The top element, which is the largest value in the queue, is then printed.

Refer to this site to understand it better:
https://www.geeksforgeeks.org/priority-queue-set-1-introduction/
