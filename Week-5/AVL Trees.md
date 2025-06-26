# AVL Tree

## What is an AVL Tree?

An AVL tree is a type of binary search tree used in computer science. It is special because it keeps itself balanced. This means it makes sure that the tree doesn't get too tall and skinny, which would make finding things slow.

In an AVL data structure, each node has a balance factor. This balance factor is the difference height between the left and right subtrees. The balance factor can only be -1, 0, or 1. If the balance factor gets outside this range, the tree does a rotation to fix itself. This keeps the tree short and wide, making it faster to search, insert, and delete items. This ensures that the tree remains approximately balanced, keeping operations like insertion, deletion, and lookup efficient with O(log n) time complexity.

---

## Properties of AVL Trees

- Balanced Tree:
An AVL tree is always balanced. This means that the heights of the left and right subtrees of any node differ by at most one.

- Height-Balanced Property:
The difference in height (also called the balance factor) between the left and right subtrees of any node is -1, 0, or 1.

- Self-Balancing:
An AVL tree automatically performs rotations to maintain balance after every insertion and deletion.

- Binary Search Tree Properties:
An AVL tree follows the properties of a binary search tree (BST). This means that for any node, the left subtree contains only nodes with values less than the node's value, and the right subtree contains only nodes with values greater than the node's value.

- Rotations:
To maintain balance, an AVL tree uses four types of rotations: left rotation, right rotation, left-right rotation, and right-left rotation

---

## Node Structure

```cpp
struct Node {
    int data;
    Node* left;
    Node* right;
    int height;

    Node(int val) {
        data = val;
        left = right = nullptr;
        height = 1;
    }
};
```

---

## Utility Functions

```cpp
int height(Node* n) {
    return n ? n->height : 0;
}

int getBalance(Node* n) {
    return n ? height(n->left) - height(n->right) : 0;
}

int max(int a, int b) {
    return (a > b) ? a : b;
}
```

---

## Rotations

### Right Rotation

```cpp
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    x->right = y;
    y->left = T2;

    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x;
}
```

### Left Rotation

```cpp
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    y->left = x;
    x->right = T2;

    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y;
}
```

---

## Insertion

```cpp
Node* insert(Node* node, int key) {
    if (node == nullptr)
        return new Node(key);

    if (key < node->data)
        node->left = insert(node->left, key);
    else if (key > node->data)
        node->right = insert(node->right, key);
    else
        return node; // No duplicates

    node->height = 1 + max(height(node->left), height(node->right));

    int balance = getBalance(node);

    if (balance > 1 && key < node->left->data)
        return rightRotate(node);

    if (balance < -1 && key > node->right->data)
        return leftRotate(node);

    if (balance > 1 && key > node->left->data) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    if (balance < -1 && key < node->right->data) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    return node;
}
```

---

## Inorder Traversal

```cpp
void inorder(Node* root) {
    if (!root) return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}
```

---

## Example

```cpp
int main() {
    Node* root = nullptr;

    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    cout << "Inorder traversal of the AVL tree is:\n";
    inorder(root);

    return 0;
}
```

---

## Output

```
Inorder traversal of the AVL tree is:
10 20 25 30 40 50
```

---
