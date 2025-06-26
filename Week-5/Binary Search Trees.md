# Binary Search Tree (BST)

## What is a Binary Search Tree?

A **Binary Search Tree (BST)** is a hierarchical data structure that extends the binary tree by maintaining order among its elements. Each node in a BST has the following properties:

- **Left Subtree Property**: The left child and its descendants contain values **less than** the current node.
- **Right Subtree Property**: The right child and its descendants contain values **greater than** the current node.
- **Recursive Structure**: Both the left and right subtrees themselves must be valid BSTs.

This structure ensures that common operations like search, insert, and delete can be performed efficiently, usually in O(log n) time for balanced trees.

---

## Node Structure

Each node contains a data field and two pointers referring to its left and right children.

```cpp
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int val) {
        data = val;
        left = nullptr;
        right = nullptr;
    }
};
```

---

## Insertion

To insert a value into the BST, we compare the value with the current node:

- If the tree is empty, the new node becomes the root.
- If the value is less than the current node, we insert it into the left subtree.
- If the value is greater, we insert it into the right subtree.
- We recursively find the correct location to maintain the BST property.

```cpp
Node* insert(Node* root, int key) {
    if (root == nullptr)
        return new Node(key);

    if (key < root->data)
        root->left = insert(root->left, key);
    else if (key > root->data)
        root->right = insert(root->right, key);

    return root;
}
```

---

## Search

To search for a value in a BST:

- Start at the root and compare the value.
- If the value equals the root's data, we return true.
- If the value is less, search the left subtree.
- If the value is more, search the right subtree.
- If we reach a null node, the value is not in the tree.

```cpp
bool search(Node* root, int key) {
    if (root == nullptr)
        return false;
    if (root->data == key)
        return true;
    if (key < root->data)
        return search(root->left, key);
    else
        return search(root->right, key);
}
```

---

## Deletion

Deleting a node from a BST involves three cases:

1. **Node is a Leaf**: Simply remove the node.
2. **Node has One Child**: Remove the node and link its parent directly to its child.
3. **Node has Two Children**: Find the inorder successor (smallest node in the right subtree), replace the node’s value with it, and then delete the successor node.

This ensures the BST properties remain intact after deletion.

```cpp
Node* minValueNode(Node* node) {
    Node* current = node;
    while (current && current->left != nullptr)
        current = current->left;
    return current;
}

Node* deleteNode(Node* root, int key) {
    if (root == nullptr) return root;

    if (key < root->data)
        root->left = deleteNode(root->left, key);
    else if (key > root->data)
        root->right = deleteNode(root->right, key);
    else {
        if (root->left == nullptr) {
            Node* temp = root->right;
            delete root;
            return temp;
        } else if (root->right == nullptr) {
            Node* temp = root->left;
            delete root;
            return temp;
        }

        Node* temp = minValueNode(root->right);
        root->data = temp->data;
        root->right = deleteNode(root->right, temp->data);
    }
    return root;
}
```

---

## Traversals

BSTs can be traversed in several ways. The most common ones include:

- **Inorder Traversal**: Visits nodes in sorted order (left → root → right). Very useful for extracting sorted data from a BST.
- **Preorder Traversal**: Visits nodes in the order (root → left → right), helpful for creating a copy of the tree.
- **Postorder Traversal**: Visits nodes in the order (left → right → root), useful for deleting or freeing the tree.
- **Level Order Traversal**: Visits nodes level by level using a queue.

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

Here is an example where we insert nodes, print the tree, and delete a node.

```cpp
int main() {
    Node* root = nullptr;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 70);
    insert(root, 20);
    insert(root, 40);
    insert(root, 60);
    insert(root, 80);

    cout << "Inorder before deletion: ";
    inorder(root);

    root = deleteNode(root, 70);

    cout << "\nInorder after deletion: ";
    inorder(root);

    return 0;
}
```

---

## Output

```
Inorder before deletion: 20 30 40 50 60 70 80
Inorder after deletion: 20 30 40 50 60 80
```
- [Range Sum of BST](https://leetcode.com/problems/range-sum-of-bst/description/)
- [Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)
- [Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/description/)
- [Minimum Distance Between BST Nodes](https://leetcode.com/problems/minimum-distance-between-bst-nodes/description/)
- [Convert BST to Greater Tree](https://leetcode.com/problems/convert-bst-to-greater-tree/description/)
- [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/)
- [Maximum Sum BST in Binary Tree](https://leetcode.com/problems/maximum-sum-bst-in-binary-tree/description/)
- [Number of Ways to Reorder Array to Get Same BST](https://leetcode.com/problems/number-of-ways-to-reorder-array-to-get-same-bst/description/)

