# Inheritance, Abstract, Polymorphism & OOP Principles

Certainly! Here are the updated markdown notes with code snippets:

### Object-Oriented programming (C#)

- C# is an object-oriented programming language.
- Object-oriented programming has four basic principles:
  1. Abstraction: Modeling entities as classes to define a system's abstract representation.
  2. Encapsulation: Hiding internal state and functionality of objects, allowing access through public functions.
  3. Inheritance: Creating new abstractions based on existing ones.
  4. Polymorphism: Implementing inherited properties or methods differently across multiple abstractions.
- The BankAccount class in the preceding tutorial demonstrates abstraction and encapsulation.

#### Create different types of accounts

```csharp
public class InterestEarningAccount : BankAccount
{
    public override void PerformMonthEndTransactions()
    {
        if (Balance > 500m)
        {
            decimal interest = Balance * 0.05m;
            MakeDeposit(interest, DateTime.Now, "apply monthly interest");
        }
    }
}

public class LineOfCreditAccount : BankAccount
{
    public override void PerformMonthEndTransactions()
    {
        if (Balance < 0)
        {
            decimal interest = -Balance * 0.07m;
            MakeWithdrawal(interest, DateTime.Now, "Charge monthly interest");
        }
    }
}

public class GiftCardAccount : BankAccount
{
    private readonly decimal _monthlyDeposit = 0m;

    public GiftCardAccount(string name, decimal initialBalance, decimal monthlyDeposit = 0)
        : base(name, initialBalance)
    {
        _monthlyDeposit = monthlyDeposit;
    }

    public override void PerformMonthEndTransactions()
    {
        if (_monthlyDeposit != 0)
        {
            MakeDeposit(_monthlyDeposit, DateTime.Now, "Add monthly deposit");
        }
    }
}
```

- Inheritance allows you to create new classes (e.g., InterestEarningAccount, LineOfCreditAccount, GiftCardAccount) that inherit methods and data from the BankAccount class.
- The derived classes can extend the base class by adding specific behavior.
- Each derived class can override a virtual method in the base class to provide its own implementation.
- The BankAccount class declares a virtual method `PerformMonthEndTransactions()` for month-end actions.

```csharp
public virtual void PerformMonthEndTransactions() { }
```

- The derived classes (e.g., InterestEarningAccount, LineOfCreditAccount, GiftCardAccount) override the `PerformMonthEndTransactions()` method with their specific implementations.

- You can use the derived classes to create instances and perform operations specific to each account type.

#### Different overdraft rules

- The LineOfCreditAccount demonstrates overriding a base method to charge a fee when the credit limit is exceeded.

```csharp
protected override Transaction? CheckWithdrawalLimit(bool isOverdrawn) =>
    isOverdrawn
    ? new Transaction(-20, DateTime.Now, "Apply overdraft fee")
    : default;
```

- By using inheritance and polymorphism, you can create and manage different types of accounts while reusing common functionality.

## Inheritance in C #

### Abstract and Virtual Methods

- **Abstract methods** are declared in a base class without providing an implementation. They must be overridden in derived classes.
- **Virtual methods** are declared in a base class with a default implementation, which can be overridden in derived classes.

### Abstract Base Classes

- An **abstract class** is declared using the `abstract` keyword and cannot be instantiated directly.
- An abstract class can contain abstract methods and non-abstract (concrete) methods.
- Derived classes must implement abstract methods from the abstract base class.

### Interfaces

- An **interface** defines a contract that classes can implement. It contains method signatures, properties, events, and indexers.
- Classes can implement multiple interfaces but can inherit from only a single base class.
- Interfaces provide a way to achieve polymorphism without a class hierarchy.

### Preventing Further Derivation

- A class can prevent other classes from inheriting from it or any of its members by using the `sealed` keyword.

### Derived Class Hiding of Base Class Members

- A derived class can hide a base class member by declaring a member with the same name and signature using the `new` modifier.
- The `new` modifier indicates that the member is not intended to be an override of the base member.

### Example

```csharp
// Base class
public class Animal
{
    public virtual void Sound()
    {
        Console.WriteLine("The animal makes a sound");
    }
}

// Derived class
public class Dog : Animal
{
    public override void Sound()
    {
        Console.WriteLine("The dog barks");
    }
}

// Usage
Animal animal = new Animal();
animal.Sound();  // Output: "The animal makes a sound"

Dog dog = new Dog();
dog.Sound();     // Output: "The dog barks"

Animal dogAsAnimal = new Dog();
dogAsAnimal.Sound();  // Output: "The dog barks"
```

In this example, we have a base class `Animal` with a virtual method `Sound()`. The derived class `Dog` overrides the `Sound()` method with its own implementation. We can create instances of both the base class and derived class. When calling the `Sound()` method, the appropriate implementation is executed based on the actual type of the object.

Note: The `virtual` keyword in the base class method and the `override` keyword in the derived class method ensure that the appropriate method implementation is called at runtime based on the actual object type.

## Abstract and Sealed Classes and Class Members in C #

### Abstract Classes and Class Members

- An **abstract class** is declared using the `abstract` keyword before the class definition.
- An abstract class cannot be instantiated and serves as a base for other classes.
- Abstract classes can have abstract methods that are declared with the `abstract` keyword before the return type.
- Abstract methods have no implementation and must be overridden in derived classes.
- Abstract classes can also have non-abstract (concrete) methods with implementations.
- Derived classes must implement all abstract methods from the abstract base class.

### Sealed Classes and Class Members

- A **sealed class** is declared using the `sealed` keyword before the class definition.
- A sealed class cannot be used as a base class and cannot be further derived.
- Sealed classes prevent inheritance and optimize runtime performance.
- In a derived class, a method, indexer, property, or event that overrides a virtual member of the base class can be declared as sealed using the `sealed` keyword.
- Sealing a member in a derived class prevents any further derived classes from overriding that member.

### Summary

Inheritance allows creating new classes that reuse, extend, and modify the behavior defined in other classes. It promotes code reuse, modularity, and polymorphism. Abstract and virtual methods enable specialization and customization of behavior, and interfaces define contracts for implementing specific capabilities. The sealed keyword prevents further derivation, and the new modifier allows hiding base class members in derived classes.

### Example

```csharp
// Abstract class
public abstract class Shape
{
    // Abstract method
    public abstract double CalculateArea();
    
    // Concrete method
    public void DisplayShapeName()
    {
        Console.WriteLine("Shape");
    }
}

// Derived class
public class Circle : Shape
{
    private double radius;
    
    public Circle(double radius)
    {
        this.radius = radius;
    }
    
    public override double CalculateArea()
    {
        return Math.PI * radius * radius;
    }
}

// Sealed class
public sealed class Square : Shape
{
    private double sideLength;
    
    public Square(double sideLength)
    {
        this.sideLength = sideLength;
    }
    
    public override double CalculateArea()
    {
        return sideLength * sideLength;
    }
}
```

In this example, we have an abstract class `Shape` with an abstract method `CalculateArea()` and a concrete method `DisplayShapeName()`. The `Circle` class is a derived class that overrides the `CalculateArea()` method. The `Square` class is a sealed derived class that also overrides the `CalculateArea()` method.

### Summary

- Abstract classes and abstract methods are used to define incomplete classes that must be implemented by derived classes.
- Sealed classes and sealed members prevent further inheritance and provide performance optimizations.
- Abstract classes serve as base classes for derived classes, while sealed classes cannot be further derived.
- Abstract methods have no implementation and must be overridden in derived classes.
- Sealed members prevent further overriding in derived classes.

## Polymorphism in C#

Polymorphism is one of the core principles of object-oriented programming, alongside encapsulation and inheritance. It allows objects of different types to be treated as objects of a common base type and enables method overriding to provide different implementations in derived classes.

#### Let's break that down!!

- "It allows objects of different types to be treated as objects of a common base type..."

Imagine you have different types of toys, like cars, dolls, and balls. These toys are all different and have their own unique features. But, let's say we have a special box called a "Toy Box" that can hold any kind of toy. The toy box treats all these different toys as if they were the same type of toy, even though they have different shapes and functions. So, even though they are different types of toys, they can be treated as if they were all "toys" when they are inside the toy box.

- "...and enables method overriding to provide different implementations in derived classes."

Now, let's say each toy can make a sound when you press a button on it. Each toy makes a different sound. For example, the car might make a "vroom" sound, the doll might say "hello," and the ball might make a bouncing sound. But all toys have a common button that can be pressed to make a sound.

When we put these toys in the toy box, we can press the button on each toy, and it will make its own unique sound. The toy box knows that even though they are all "toys," each one has its own way of making a sound. This is like method overriding. Each toy class (derived class) provides its own way of making a sound by overriding a method defined in the base class (toy box).

So, in simpler terms, polymorphism is like putting different types of toys in a toy box and treating them as if they were all "toys." It also allows each toy to have its own unique way of doing something, like making a sound, even though they are all treated as the same type of toy.

### Runtime Polymorphism

- At runtime, objects of a derived class can be treated as objects of a base class.
- This enables objects to be used interchangeably in method parameters, collections, or arrays.
- The object's declared type is no longer identical to its runtime type.
- This polymorphism is achieved through inheritance.

### Virtual Methods

- Base classes can define and implement **virtual methods**.
- Derived classes can **override** these virtual methods to provide their own implementations.
- At runtime, the CLR (Common Language Runtime) looks up the object's runtime type and invokes the appropriate override of the virtual method.
- The base class can also provide a default implementation for the virtual method.
- Virtual methods allow working with groups of related objects in a uniform way.

### Example: Drawing Application

To illustrate polymorphism, consider a drawing application that supports different types of shapes (e.g., rectangles, circles, triangles). The application needs to update and draw these shapes without knowing their specific types at compile time.

- Create a base class `Shape` with a virtual method `Draw()` and derived classes `Rectangle`, `Circle`, and `Triangle`.
- Each derived class overrides the `Draw()` method with its own implementation.
- Use a `List<Shape>` to store different shape objects.
- Iterate through the list and call the `Draw()` method on each shape.
- The runtime polymorphism ensures that the appropriate implementation is invoked for each shape.

```csharp
using System;
using System.Collections.Generic;

public class Shape
{
    public virtual void Draw()
    {
        Console.WriteLine("Drawing a generic shape");
    }
}

public class Rectangle : Shape
{
    public override void Draw()
    {
        Console.WriteLine("Drawing a rectangle");
    }
}

public class Circle : Shape
{
    public override void Draw()
    {
        Console.WriteLine("Drawing a circle");
    }
}

public class Triangle : Shape
{
    public override void Draw()
    {
        Console.WriteLine("Drawing a triangle");
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        List<Shape> shapes = new List<Shape>
        {
            new Rectangle(),
            new Circle(),
            new Triangle()
        };

        foreach (Shape shape in shapes)
        {
            shape.Draw();
        }
    }
}
```

### Summary

- Polymorphism in C# allows objects of different types to be treated as objects of a common base type.
- Virtual methods enable derived classes to override and provide their own implementations of methods defined in the base class.
- Runtime polymorphism is achieved through inheritance and method overriding.
- Polymorphism promotes code reusability, flexibility, and extensibility in object-oriented programming.