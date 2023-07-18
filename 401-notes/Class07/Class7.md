# Interfaces - Define Behavior for Multiple Types

An interface in C# contains definitions for a group of related functionalities that a non-abstract class or a struct must implement. Unlike abstract classes, interfaces cannot declare instance data such as fields or auto-implemented properties. However, they can define static methods with an implementation or provide default implementations for members.

The primary use of interfaces in C# is to include behavior from multiple sources in a class since C# does not support multiple inheritance of classes. Additionally, interfaces are necessary to simulate inheritance for structs, as they cannot directly inherit from another struct or class.

To define an interface, use the `interface` keyword, as shown in the following example:

```csharp
interface IEquatable<T>
{
    bool Equals(T obj);
}
```

Interface names in C# should begin with a capital "I" as a convention.

Any class or struct that implements the `IEquatable<T>` interface must provide a definition for the `Equals` method, matching the signature specified in the interface. This allows an instance of the class to determine whether it is equal to another instance of the same class.

It's important to note that an interface can be implemented by multiple classes or structs, but a class can only inherit from a single class.

Interfaces can contain various member types, including instance methods, properties, events, indexers, and static members. However, interfaces cannot contain instance fields, constructors, or finalizers. Beginning with C# 11, interface members (excluding fields) may be static abstract. By default, interface members are public, but you can specify accessibility modifiers such as public, protected, internal, private, protected internal, or private protected. A private member must have a default implementation.

To implement an interface member, the corresponding member in the implementing class must be public, non-static, and have the same name and signature as the interface member.

When an interface declares static members, a type implementing that interface may also declare static members with the same signature. However, the static member declared in a type does not override the static member declared in the interface.

A class or struct implementing an interface must provide an implementation for all declared members without a default implementation provided by the interface. If a base class implements an interface, any derived class will inherit that implementation.

Here's an example implementation of the `IEquatable<T>` interface:

```csharp
public class Car : IEquatable<Car>
{
    public string? Make { get; set; }
    public string? Model { get; set; }
    public string? Year { get; set; }

    // Implementation of IEquatable<T> interface
    public bool Equals(Car? car)
    {
        return (this.Make, this.Model, this.Year) == (car?.Make, car?.Model, car?.Year);
    }
}
```

In this example, the `Car` class implements the `IEquatable<Car>` interface and provides an implementation for the `Equals` method.

Interfaces also allow properties and indexers of a class to define extra accessors beyond what's defined in the interface. If explicit implementation is used, the accessors must match. For more information about explicit implementation, refer to "Explicit Interface Implementation and Interface Properties."

`Interfaces can inherit from one or more interfaces, and the derived interface inherits members from its base interfaces`. A class implementing a derived interface must implement all members of the derived interface and its base interfaces. A class can be implicitly converted to the derived interface or any of its base interfaces. A class might include an interface multiple times through base classes or other interfaces, but it can provide an implementation of an interface only once as part of its definition (`class ClassName : InterfaceName`). If the interface is inherited through a base class that implements it, the base class provides the implementation. However, the derived class can choose to reimplement any virtual interface members instead of using the inherited implementation. When an interface declares a default implementation for a method, any class implementing that interface inherits that implementation (the class instance needs to be cast to the interface type to access the default implementation on the interface member).

A base class can also implement interface members using virtual members, allowing a derived class to override and change the interface behavior. For more information about virtual members, refer to "Polymorphism."

## Interfaces Summary

An interface in C# has the following properties:

- In versions earlier than C# 8.0, an interface is similar to an abstract base class with only abstract members. A class or struct implementing the interface must implement all its members.
- Starting with C# 8.0, an interface may define default implementations for some or all of its members. A class or struct implementing the interface is not required to implement members with default implementations.
- An interface cannot be instantiated directly. Its members are implemented by any class or struct that implements the interface.
- A class or struct can implement multiple interfaces. It can also inherit a base class and implement one or more interfaces.

Markdown notes for the above text:

- An interface defines a set of related functionalities that a class or struct must implement.
- C# doesn't support multiple inheritance, so interfaces are used to include behavior from multiple sources.
- Interfaces can contain static methods with implementations and provide default implementations for members.
- Interfaces cannot declare instance data such as fields or auto-implemented properties.
- Interface names usually start with a capital "I".
- A class or struct implementing an interface must provide definitions for all interface members.
- Interfaces can contain instance methods, properties, events, indexers, and static members.
- Interfaces cannot contain instance fields, constructors, or finalizers.
- Interface members are public by default and can have explicit accessibility modifiers.
- A class can implement multiple interfaces but can inherit from only one class.
- Interfaces can inherit from other interfaces, and a class implementing a derived interface must implement all members of the derived interface and its base interfaces.
- Base classes can provide implementations for interface members, and derived classes can choose to override them.
- Properties and indexers in a class can have extra accessors beyond what's defined in the interface.
- An interface cannot be instantiated directly; its members are implemented by implementing classes or structs.


## The Value and Correct Use of Interfaces

**Problem Solved by Interfaces**

Interfaces aim to separate the usage of something from its implementation in programming languages like C# and Java. The primary problem interfaces solve is enabling code to work with different implementations of a set of responsibilities without explicitly handling each implementation.

The goal is to write code in such a way that a `Driver` class can have a `Drive` method that can be used to drive any type of vehicle, such as a car, boat, or any other class that implements the `IDriveable` interface. The `Driver` class should not have separate methods for each type of vehicle, but rather rely on a generic interface for driving any object that supports the necessary operations.

**Interfaces as Contracts**

Interfaces serve as contracts in which a class that implements an interface is obligated to provide all the methods defined in that interface. When a class implements an interface, it does not mean the class *is* the interface; rather, it indicates that the class *implements* the interface. Therefore, interfaces do not fully describe the functionality of a class.

A class can implement multiple interfaces because each interface represents a specific contract that the class can fulfill.

**Interfaces Are Always Implemented by More Than One Class**

Interfaces are ideally implemented by more than one class, as they are designed to solve specific problems related to interaction and abstraction. While it may be tempting to create an interface for every class, it is important to apply the "You Ain't Gonna Need It" (YAGNI) principle. Only when there is a genuine need to interact with multiple implementations of a contract should an interface be introduced.

Creating interfaces prematurely, before having multiple classes that need to fulfill the same contract, anticipates a future problem that may never arise. It is essential to avoid adding unnecessary complexity to the codebase.

While there may be cases where a class implements an interface that no other class implements, it indicates a misuse of interfaces. It is crucial to ensure that interfaces are implemented by multiple classes to solve real problems as they arise.

**Testing and Dependency Injection**

Unit testing and dependency injection are common reasons for incorrect interface usage. Creating interfaces solely for mocking or dependency injection purposes introduces an additional level of indirection and can lead to unnecessary coupling.

While there is no easy solution to unit testing or dependency injection without interface abuse, the focus should be on reducing dependencies and splitting classes apart rather than simply creating interfaces for the sake of injecting them.

The challenge lies in the fact that interfaces are part of the language, while unit testing and dependency injection are external concepts. Trying to fit these concepts into the language using interfaces as a workaround dilutes the potency of interfaces. Instead, a language-supported mechanism that allows easy replacement of concrete class implementations at runtime would be more beneficial.

Markdown notes for the above text:

- Interfaces separate usage from implementation in programming languages like C# and Java.
- Interfaces enable code to work with different implementations without explicitly handling each one.
- Interfaces serve as contracts, specifying that a class implementing the interface must provide all defined methods.
- Classes implementing interfaces are not the same as the interfaces themselves.
- Interfaces should be implemented by more than one class to solve real problems.
- Prematurely creating interfaces before a genuine need arises violates the YAGNI principle.
- Unit testing and dependency injection often lead to interface abuse.
- Dependency injection is most beneficial when it allows choosing different implementations of an interface.
- Creating interfaces solely for mocking or injecting the only implementation introduces unnecessary indirection.
- The challenge is that interfaces are part of the language, while unit testing and dependency injection are external concepts.
- An ideal solution would involve a language-supported mechanism for easy replacement of concrete class implementations at runtime.

