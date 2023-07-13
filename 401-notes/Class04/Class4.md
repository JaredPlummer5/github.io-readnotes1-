# Classes & Memory Management

## Classes in Programming

### Reference Types

- A type defined as a class is a reference type.
- When a variable of a reference type is declared, it contains the value null until you create an instance of the class.
- Enough memory is allocated on the managed heap for the specific object when it's created, and the variable holds only a reference to the object's location.

```csharp
//Declaring an object of type MyClass.
MyClass mc = new MyClass();

//Declaring another object of the same type, assigning it the value of the first object.
MyClass mc2 = mc;
```

### Declaring Classes

- Classes are declared using the `class` keyword followed by a unique identifier.

```csharp
//[access modifier] - [class] - [identifier]
public class Customer
{
   // Fields, properties, methods and events go here...
}
```

### Creating Objects

- A class defines a type of object, but it is not an object itself. An object is a concrete entity based on a class, referred to as an instance of a class.
- Objects are created using the `new` keyword followed by the class name.

```csharp
Customer object1 = new Customer();
```

### Constructors and Initialization

- When creating an instance of a type, it's important to ensure its fields and properties are initialized to useful values.
- Initialization can be done in several ways:
  - Accept default values.
  - Field initializers.
  - Constructor parameters.
  - Object initializers.

```csharp
// Using field initializers
public class Container
{
    private int _capacity = 10;
}

// Using constructor parameters
public class Container
{
    private int _capacity;

    public Container(int capacity) => _capacity = capacity;
}
```

### Class Inheritance

- Classes in C# fully support inheritance, a fundamental characteristic of object-oriented programming.
- A class can inherit from any other class that isn't defined as sealed and can be inherited by other classes.

```csharp
public class Manager : Employee
{
    // Employee fields, properties, methods and events are inherited
    // New Manager fields, properties, methods and events go here...
}
```

- A class in C# can directly inherit from one base class, but indirectly inherit multiple base classes because a base class may inherit from another class.
- A class can directly implement one or more interfaces. 

### Abstract and Sealed Classes

- An abstract class contains abstract methods that have a signature definition but no implementation. They can't be instantiated.
- A sealed class doesn't allow other classes to derive from it.

### Partial Classes

- Class definitions can be split between different source files.

## Constructors in C# Programming

### Constructor Syntax

- A constructor is a method whose name is the same as the name of its type.
- It does not include a return type and its method signature includes only an optional access modifier, the method name and its parameter list.

```csharp
public class Person
{
   private string last;
   private string first;

   public Person(string lastName, string firstName)
   {
      last = lastName;
      first = firstName;
   }

   // Remaining implementation of Person class.
}
```

- If a constructor can be implemented as a single statement, an expression body definition can be used.

```csharp
public class Location
{
   private string locationName;

   public Location(string name) => Name = name;

   public string Name
   {
      get => locationName;
      set => locationName = value;
   }
}
```

### Static Constructors

- A class or struct can also have a static constructor, which initializes static members of the type.
- Static constructors are parameterless.
- If a static constructor is not provided to initialize static fields, the C# compiler initializes static fields to their default value.

```csharp
public class Child : Person
{
   private static int maximumAge;

   public Child(string lastName, string firstName) : base(lastName, firstName)
   { }

   static Child() => maximumAge = 18;

   // Remaining implementation of Child class.
}
```

### Order of Actions in Constructor

When a new instance is initialized, several actions take place in the following order:

1. Instance fields are set to 0.
2. Field initializers run in the most derived type.
3. Base type field initializers run, starting with the direct base through each base type to `System.Object`.
4. Base instance constructors run, starting with `Object.Object` through each base class to the direct base class.
5. The instance constructor for the type runs.
6. If the expression includes any object initializers, they run after the instance constructor runs in the textual order.

If a new instance of a struct is set to its default value, all instance fields are set to 0. If the static constructor hasn't run, it runs before any of the instance constructor actions take place.

## Properties in C# Programming

### Overview

A property in C# is a member that provides a mechanism to read, write, or compute the value of a private field. Properties can be used as if they're public data members but they're actually special methods called accessors.

- A `get` property accessor is used to return the property value.
- A `set` property accessor is used to assign a new value. 
- An `init` property accessor, available from C# 9 and later, is used to assign a new value only during object construction.

Properties can be read-write, read-only, or write-only depending on the presence of get and/or set accessors.

### Properties with Backing Fields

A common pattern is to use a private backing field to store the value of a property. The get accessor returns the value of the field and the set accessor can perform validation before assigning a value to the field.

```csharp
public class TimePeriod
{
    private double _seconds;

    public double Hours
    {
        get { return _seconds / 3600; }
        set
        {
            if (value < 0 || value > 24)
                throw new ArgumentOutOfRangeException(nameof(value),
                      "The valid range is between 0 and 24.");

            _seconds = value * 3600;
        }
    }
}
```

### Expression Body Definitions

Property accessors can be implemented as expression-bodied members when they consist of single-line statements.

```csharp
public class Person
{
    private string _firstName;
    private string _lastName;

    public Person(string first, string last)
    {
        _firstName = first;
        _lastName = last;
    }

    public string Name => $"{_firstName} {_lastName}";
}
```

### Auto-implemented Properties

Auto-implemented properties can be used to simplify code when property get and set accessors just assign a value to or retrieve a value from a backing field without including any extra logic.

```csharp
public class SaleItem
{
    public string Name
    { get; set; }

    public decimal Price
    { get; set; }
}
```

From C# 11, the `required` keyword can be added to force client code to initialize any property or field:

```csharp
public class SaleItem
{
    public required string Name
    { get; set; }

    public required decimal Price
    { get; set; }
}

var item = new SaleItem { Name = "Shoes", Price = 19.95m };
```

## Memory Management in .NET: Stack vs Heap

Memory management in .NET consists of two main components - the Stack and the Heap. Understanding these concepts can lead to better optimization of your applications.

### Stack vs Heap

- The **Stack** is responsible for keeping track of what's executing in our code. It's like a series of boxes stacked one on top of the next, each box representing a method call (a frame).
- The **Heap**, on the other hand, is responsible for keeping track of our data objects. Unlike the Stack, there are no constraints as to what can be accessed, allowing us to grab what we need quickly. It requires garbage collection to keep clean.

### Types of Variables

There are four main types of variables that we'll be putting in the Stack and Heap as our code executes: Value Types, Reference Types, Pointers, and Instructions.

1. **Value Types**: These are types like bool, byte, char, decimal, double, enum, float, int, long, sbyte, short, struct, uint, ulong, and ushort.

2. **Reference Types**: These include class, interface, delegate, object, and string.

3. **Pointers**: Pointers, or References, are used to access other variables in memory. They are managed by the Common Language Runtime (CLR) and either point to a memory address or are null.

### Deciding What Goes Where

- A Reference Type always goes on the Heap.

- Value Types and Pointers go where they were declared. If a Value Type is declared outside of a method, but inside a Reference Type, it will be placed within the Reference Type on the Heap.

### Garbage Collection (GC)

The GC cleans up objects in the Heap that are not being accessed by the main program when our program reaches a certain memory threshold. This can be a performance heavy operation and hence understanding and optimizing what's in your Stack and Heap is important.

### Understanding Value Types vs Reference Types

- With Value Types, you are dealing with the value itself.

- With Reference Types, you are dealing with pointers to the type.

This means that changing the value of a Reference Type variable will also change the value of all other variables that point to the same object in the Heap.

Understanding these differences between Value Type and Reference Type variables in C# provides a basic understanding of what a Pointer is and when it is used. Further discussion on memory management and method parameters will follow in the next part of this series.


## Comparing Garbage Collection in C# and Lifecycle of Household Items

### 1. **Acquisition (Creating the Object / Buying an Item)**

In C#, we acquire a new object by creating it with the `new` keyword. This can be compared to purchasing a new household item.

```CSharp
// In C#
MyObject obj = new MyObject(); // create a new object
```

**Household Item Equivalent**: You buy a new toaster for your kitchen.

---

### 2. **Usage (Using the Object / Using the Item)**

Once we have an object, we can call its methods, access its properties, and basically use it to perform actions.

```CSharp
// In C#
obj.DoSomething(); // use the object
```

**Household Item Equivalent**: You use your toaster every morning to prepare your breakfast.

---

### 3. **Discarding (Removing References / Stop Using the Item)**

Once we're done using an object in C#, we can remove all references to it. This means setting all variables that were pointing to it to `null`. 

```CSharp
// In C#
obj = null; // discard the object by removing references
```

**Household Item Equivalent**: One day, your toaster breaks down or you simply decide to stop using it. You unplug it and place it in your garage, no longer using it for breakfast.

---

### 4. **Garbage Collection (Freeing Up Memory / Throwing Away the Item)**

The Garbage Collector (GC) in C# is an automatic memory manager. When an object is no longer being used (there are no references to it), the GC will eventually find it and free up the memory that it was using. 

*Note: You don't have control over exactly when the GC will do this.*

**Household Item Equivalent**: When the garage is full or you decide to clean up, you throw away the old toaster, freeing up space. This is similar to how the Garbage Collector works. When memory starts getting full, or at certain times, it cleans up by getting rid of the "unused" objects.

---

### 5. **Reallocation (Reusing Freed Memory / Buying a New Item)**

Once the GC has freed up some memory, it can be used to create new objects. This is similar to using the space that was freed up when you threw away the toaster to store something new.

```CSharp
// In C#
MyOtherObject newObj = new MyOtherObject(); // create a new object in the freed memory
```

**Household Item Equivalent**: You use the space in your garage where the old toaster was to store a new blender.

---

The above steps show how the lifecycle of an object in C# is very similar to the lifecycle of normal household items. This comparison can help make the concept of Garbage Collection in C# easier to understand.
