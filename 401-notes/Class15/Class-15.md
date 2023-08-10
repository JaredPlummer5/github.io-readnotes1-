# Trees

## Common Terminology

- **Node**: A Tree node is a component that may contain its values and references to other nodes.
- **Root**: The root is the node at the beginning of the tree.
- **K**: A number that specifies the maximum number of children any node may have in a k-ary tree. In a binary tree, `k = 2`.
- **Left**: A reference to one child node, in a binary tree.
- **Right**: A reference to the other child node, in a binary tree.
- **Edge**: The edge in a tree is the link between a parent and child node.
- **Leaf**: A leaf is a node that does not have any children.
- **Height**: The height of a tree is the number of edges from the root to the furthest leaf.

#### Traversals

Traversing a tree allows us to search for a node, print out the contents of a tree, and more. There are two categories of traversals:

1. **Depth First**

2. **Breadth First**

### Depth First

Depth first traversal prioritizes going through the depth (height) of the tree first. Methods for depth first traversal:

- **Pre-order**: `root >> left >> right`
- **In-order**: `left >> root >> right`
- **Post-order**: `left >> right >> root`

### Pre-order Traversal

Here's the pseudocode for pre-order traversal:

```plaintext
ALGORITHM preOrder(root)
  OUTPUT <-- root.value
  if root.left is not NULL
      preOrder(root.left)
  if root.right is not NULL
      preOrder(root.right)
```

## Breadth First

Breadth-first traversal iterates through the tree by going through each level of the tree node-by-node. Traditionally, it uses a queue to traverse the width/breadth of the tree.

## Traversal Pseudocode

- **Pre-order**

```plaintext
ALGORITHM preOrder(root)
    OUTPUT <-- root.value
    if root.left is not Null
        preOrder(root.left)
    if root.right is not NULL
        preOrder(root.right)
```

- **In-order**

```plaintext
ALGORITHM inOrder(root)
    if root.left is not NULL
        inOrder(root.left)
    OUTPUT <-- root.value
    if root.right is not NULL
        inOrder(root.right)
```

- **Post-order**

```plaintext
ALGORITHM postOrder(root)
    if root.left is not NULL
        postOrder(root.left)
    if root.right is not NULL
        postOrder(root.right)
    OUTPUT <-- root.value
```
