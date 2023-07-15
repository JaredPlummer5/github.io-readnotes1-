# Linked Lists in C#

## An Analogy: The Train Cars

Imagine a long train traveling on tracks. Each train car is connected to the one in front and the one behind it, forming a chain-like structure. This connection between the cars allows the train to move as a single unit, and you can add or remove cars from the train at any point. In a similar way, a linked list in C# is a data structure where each element (node) contains a value and a reference to the next node, creating a sequence of connected nodes.

## Detail in Depth

In a linked list, each node contains two main components: `the value it holds and a reference to the next node in the sequence`. The value can be any data type (e.g., an integer, string, or custom object) and represents the actual information stored in the node. The reference to the next node, often called the "next" pointer or "next" reference, is what establishes the link between nodes.

The first node in the linked list is called the head, and it serves as the starting point for traversing the list. The last node, whose "next" reference is null, is known as the tail and indicates the end of the list.

To traverse a linked list, you start at the head and follow the "next" references until you reach the desired node or the end of the list (tail). Each node in the list only knows about the next node, so there is no direct way to access a specific node from any arbitrary position. You have to iterate through the nodes sequentially.

Unlike arrays, linked lists do not require contiguous memory allocation. Each node can be scattered across the computer's memory, and the "next" reference connects them together.

## WHY, WHAT, HOW Structure

**Why use linked lists?**

Linked lists provide several advantages over other data structures, such as arrays:

1. **Dynamic Size:** Linked lists can grow or shrink dynamically without the need for resizing or copying elements.
2. **Efficient Insertions and Deletions:** Adding or removing elements in a linked list can be done in constant time O(1) by adjusting the "next" references.
3. **Memory Efficiency:** Linked lists use memory efficiently since they only require space for the individual elements and their connecting references.

**What are linked lists?**

A linked list is a data structure consisting of a sequence of nodes, where each node holds a value and a reference to the next node.

**How to implement a linked list in C#?**

Here's a step-by-step guide to implementing a linked list in C#:

1. Create a Node class that represents a single node in the linked list. The class should have two properties: one to store the value and another to store the reference to the next node.
2. Create a LinkedList class that manages the linked list. This class should have a property to store the head (first node) and methods to perform operations such as inserting, deleting, and traversing the list.
3. Implement the methods in the LinkedList class to handle various operations. For example, the Insert method should create a new node, adjust the "next" references, and update the head or tail if necessary.
4. Test your implementation by creating an instance of the LinkedList class, adding nodes with values, and verifying the correctness of the operations.

## Example: Tutorial

Let's walk through an example to illustrate the implementation of a linked list in C#.

```csharp
class Node
{
    public int Value { get; set; }
    public Node Next { get; set; }
}

class LinkedList
{
    private Node head;

    public void Insert(int value)
    {
        Node newNode = new Node { Value = value };

        if (head == null)
        {
            head = newNode;
        }
        else
        {
            Node current = head;
            while (current.Next != null)
            {
                current = current.Next;
            }
            current.Next = newNode;
        }
    }

    public void Print()
    {
        Node current = head;
        while (current != null)
        {
            Console.Write(current.Value + " ");
            current = current.Next;
        }
        Console.WriteLine();
    }
}

// Usage example
LinkedList list = new LinkedList();
list.Insert(10);
list.Insert(20);
list.Insert(30);
list.Print();
```

In this example, we create a simple linked list with the ability to insert nodes and print the list. The Node class represents a node with an integer value and a reference to the next node. The LinkedList class manages the list and provides methods to insert nodes at the end and print the list. The `Insert` method checks if the list is empty (head is null) and sets the new node as the head. Otherwise, it iterates through the list until the last node and appends the new node to the end.

The output of the example will be:

```
10 20 30
```

## Vocabulary/Definition List

- Linked List: A data structure that represents a sequence of connected nodes, where each node contains a value and a reference to the next node.
- Node: A single element in a linked list that stores a value and a reference to the next node.
- Head: The first node in a linked list.
- Tail: The last node in a linked list, whose "next" reference is null.
- Next: A reference in a node that points to the next node in the linked list.
- Insertion: The process of adding a new node to a linked list.
- Deletion: The process of removing a node from a linked list.
- Traversal: The act of iterating through a linked list by following the "next" references.

## Cheat Sheet

- Creating a Node class:

```csharp
class Node
{
    public int Value { get; set; }
    public Node Next { get; set; }
}
```

- Creating a LinkedList class:

```csharp
class LinkedList
{
    private Node head;

    // Insertion method
    public void Insert(int value)
    {
        // Implementation code here
    }

    // Deletion method
    public void Delete(int value)
    {
        // Implementation code here
    }

    // Traversal method


    public void Print()
    {
        // Implementation code here
    }
}
```

- Inserting a node at the end of the linked list:

```csharp
public void Insert(int value)
{
    Node newNode = new Node { Value = value };

    if (head == null)
    {
        head = newNode;
    }
    else
    {
        Node current = head;
        while (current.Next != null)
        {
            current = current.Next;
        }
        current.Next = newNode;
    }
}
```

- Deleting a node from the linked list:

```csharp
public void Delete(int value)
{
    if (head == null)
    {
        return;
    }

    if (head.Value == value)
    {
        head = head.Next;
        return;
    }

    Node current = head;
    while (current.Next != null)
    {
        if (current.Next.Value == value)
        {
            current.Next = current.Next.Next;
            return;
        }
        current = current.Next;
    }
}
```

- Traversing and printing the linked list:

```csharp
public void Print()
{
    Node current = head;
    while (current != null)
    {
        Console.Write(current.Value + " ");
        current = current.Next;
    }
    Console.WriteLine();
}
```

## Diagram: Linked List Visualization

```
+---+    +---+    +---+    +----+
| 1 | -> | 2 | -> | 3 | -> | 4 | -> null
+---+    +---+    +---+    +----+
```

This diagram represents a linked list with four nodes, numbered 1 to 4. Each node has a value and a reference to the next node. The last node's reference is null, indicating the end of the list.

## Conversation between Linked List Nodes

**Node A**: Hey, I heard you're a part of the linked list too! What's your value?

**Node B**: Yeah, I am! My value is 42. What about you?

**Node A**: Cool! Mine is 17. Do you know who comes after us?

**Node B**: Sure, it's Node C. I have a reference to it. Want me to introduce you?

**Node A**: Definitely! Let's keep this chain going. Hello, Node C!

**Node C**: Hi there! Nice to meet you, Node A. And hello, Node B! I've heard a lot about you two.

**Node B**: Likewise, Node C. We're forming a great linked list here, aren't we?

**Node C**: Absolutely! We're like a team, connected and ready to store and share data efficiently.

## Fill-in-the-Blank Worksheet: Linked List

Fill in the blanks to complete the sentences:

1. In a linked list, each node contains a __________ and a reference to the __________ node.
2. The first node in a linked list is called the ________.
3. The last node in a linked list, whose "next" reference is null, is known as the ________.
4. To traverse a linked list, you start at the ________ and follow the "next" references.
5. Linked lists provide efficient _________ and _________ operations.
6. Unlike arrays, linked lists do not require __________ memory allocation.
7. The process of adding a new node to a linked list is called _________.
8. The process of removing a node from a linked list is called _________.
9. The act of iterating through a linked list by following the "next" references is known as _________.

Answers:

1. value, next
2. head
3. tail
4. head
5. insertion, deletion
6. contiguous
7. insertion
8. deletion
9. traversal