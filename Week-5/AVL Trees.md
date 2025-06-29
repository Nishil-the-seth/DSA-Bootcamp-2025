# AVL Trees

An **AVL Tree** is a self-balancing Binary Search Tree (BST) where the difference between heights of left and right subtrees cannot be more than one for all nodes. It is named after its inventors Adelson-Velsky and Landis.

Balancing is maintained through **rotations** that occur during insertions and deletions.

---

## Properties

1. **Binary Search Tree Property**:
   - For each node, values in the left subtree are less than the node’s value, and values in the right subtree are greater.

2. **Balance Factor**:
   - Defined as the difference in height between the left and right subtree.
   - `BalanceFactor = height(left subtree) - height(right subtree)`
   - Must be -1, 0, or +1 for all nodes.

3. **Height-Balanced**:
   - Ensures operations like insertion, deletion, and look-up all occur in **O(log n)** time.

---

## Rotations in AVL Tree

To maintain balance, AVL Trees use **four types of rotations**:

### 1. Right Rotation (LL Rotation)
Used when a node is inserted into the **left subtree of the left child**.

### 2. Left Rotation (RR Rotation)
Used when a node is inserted into the **right subtree of the right child**.

### 3. Left-Right Rotation (LR Rotation)
Used when a node is inserted into the **right subtree of the left child**.

### 4. Right-Left Rotation (RL Rotation)
Used when a node is inserted into the **left subtree of the right child**.

---

## AVL Tree Operations

### 1. Insertion
- Insert like a normal BST.
- Update the height of the ancestor nodes.
- Check balance factor.
- Perform necessary rotations if unbalanced.

### 2. Deletion
- Delete like a normal BST.
- Update the height of the ancestor nodes.
- Rebalance the tree using rotations if required.

---

## Time Complexity

| Operation | Time Complexity |
|-----------|------------------|
| Search    | O(log n)         |
| Insert    | O(log n)         |
| Delete    | O(log n)         |

---

## C++ Implementation

```cpp
#include <iostream>
using namespace std;

class Node {
public:
    int key, height;
    Node* left;
    Node* right;

    Node(int value) {
        key = value;
        height = 1;
        left = right = nullptr;
    }
};

int height(Node* N) {
    return N ? N->height : 0;
}

int getBalance(Node* N) {
    return N ? height(N->left) - height(N->right) : 0;
}

int max(int a, int b) {
    return (a > b) ? a : b;
}

Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    x->right = y;
    y->left = T2;

    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x;
}

Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    y->left = x;
    x->right = T2;

    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y;
}

Node* insert(Node* node, int key) {
    if (!node)
        return new Node(key);

    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    else
        return node;

    node->height = 1 + max(height(node->left), height(node->right));

    int balance = getBalance(node);

    if (balance > 1 && key < node->left->key)
        return rightRotate(node);
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);
    if (balance > 1 && key > node->left->key) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }
    if (balance < -1 && key < node->right->key) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    return node;
}

void inOrder(Node* root) {
    if (root) {
        inOrder(root->left);
        cout << root->key << " ";
        inOrder(root->right);
    }
}

int main() {
    Node* root = nullptr;

    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    inOrder(root); // Output: 10 20 25 30 40 50

    return 0;
}
