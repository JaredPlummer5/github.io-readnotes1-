# Stacks and Queues in C#

## Stack

A `Stack` is a data structure which follows the LIFO (Last In First Out) principle. You can think of it like a stack of plates. The last plate you put on the stack is the first one you would take off.

### Methods
* `Push(T)`: Adds an object to the top of the Stack.
* `Pop()`: Removes and returns the object at the top of the Stack.
* `Peek()`: Returns the object at the top of the Stack without removing it.
* `Clear()`: Removes all objects from the Stack.

### Example
```csharp
Stack<int> stack = new Stack<int>();

stack.Push(1);
stack.Push(2);
stack.Push(3);

Console.WriteLine(stack.Pop()); // Outputs 3
Console.WriteLine(stack.Peek()); // Outputs 2
```

## Queue

A `Queue` is a data structure which follows the FIFO (First In First Out) principle. You can think of it like a queue of people. The first person that gets in the queue is the first one who gets out.

### Methods
* `Enqueue(T)`: Adds an object to the end of the Queue.
* `Dequeue()`: Removes and returns the object at the beginning of the Queue.
* `Peek()`: Returns the object at the beginning of the Queue without removing it.
* `Clear()`: Removes all objects from the Queue.

### Example
```csharp
Queue<int> queue = new Queue<int>();

queue.Enqueue(1);
queue.Enqueue(2);
queue.Enqueue(3);

Console.WriteLine(queue.Dequeue()); // Outputs 1
Console.WriteLine(queue.Peek()); // Outputs 2
```

In both examples, replace `int` with the type you want to store in your Stack or Queue.