# Collections (C#)

## Using a Simple Collection

The examples in this section demonstrate the usage of the `List<T>` class, which is a generic collection that allows you to work with a strongly typed list of objects.

```csharp
// Create a list of strings.
var salmons = new List<string>();
salmons.Add("chinook");
salmons.Add("coho");
salmons.Add("pink");
salmons.Add("sockeye");

// Iterate through the list.
foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");
}
// Output: chinook coho pink sockeye
```

You can also use a collection initializer to add elements to the list directly:

```csharp
// Create a list of strings using a collection initializer.
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };

// Iterate through the list.
foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");
}
// Output: chinook coho pink sockeye
```

You can iterate through the elements of a list using a `for` loop:

```csharp
// Create a list of strings using a collection initializer.
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };

for (var index = 0; index < salmons.Count; index++)
{
    Console.Write(salmons[index] + " ");
}
// Output: chinook coho pink sockeye
```

You can remove elements from a list using the `Remove` method by specifying the object to remove:

```csharp
// Create a list of strings using a collection initializer.
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };

// Remove an element from the list by specifying the object.
salmons.Remove("coho");

// Iterate through the list.
foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");
}
// Output: chinook pink sockeye
```

You can also use a `for` loop to remove elements from a list, but you need to iterate in descending order to avoid issues with index positions:

```csharp
var numbers = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };

// Remove odd numbers.
for (var index = numbers.Count - 1; index >= 0; index--)
{
    if (numbers[index] % 2 == 1)
    {
        numbers.RemoveAt(index);
    }
}

// Iterate through the list using a lambda expression in the ForEach method.
numbers.ForEach(number => Console.Write(number + " "));
// Output: 0 2 4 6 8
```

You can define your own class for elements in the list:

```csharp
private static void IterateThroughList()
{
    var theGalaxies = new List<Galaxy>
    {
        new Galaxy() { Name="Tadpole", MegaLightYears=400},
        new Galaxy() { Name="Pinwheel", MegaLightYears=25},
        new Galaxy() { Name="Milky Way", MegaLightYears=0},
        new Galaxy() { Name="Andromeda", MegaLightYears=3}
    };

    foreach (Galaxy theGalaxy in theGalaxies)
    {
        Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears);
    }
}

public class Galaxy
{
    public string Name { get; set; }
    public int MegaLightYears { get; set; }
}
```

## Kinds of Collections

In .NET, there are various kinds of collections available for different purposes. Some commonly used collection classes include:

### System.Collections.Generic Classes

You can use generic collections from the `System.Collections.Generic` namespace when you want to work with a collection of objects that have the same data type. The generic collections provide type safety and prevent adding elements of different types. Some commonly used generic collection classes are:

- `Dictionary<TKey, TValue>`: Represents a collection of key/value pairs organized based on the key.
- `List<T>`: Represents a list of objects that can be accessed by index and provides methods for searching, sorting, and modifying lists.
- `Queue<T>`: Represents a first-in, first-out (FIFO) collection of objects.
- `SortedList<TKey, TValue>`: Represents a collection of key/value pairs that are sorted by the key.
- `Stack<T>`: Represents a last-in, first-out (LIFO) collection of objects.

### System.Collections.Concurrent Classes

The `System.Collections.Concurrent` namespace provides collections designed for efficient thread-safe operations in scenarios where multiple threads access the collection concurrently. Some commonly used concurrent collection classes are:

- `BlockingCollection<T>`: Provides blocking and bounding capabilities for adding and removing elements.
- `ConcurrentDictionary<TKey, TValue>`: Represents a thread-safe collection of key/value pairs.
- `ConcurrentQueue<T>`: Represents a thread-safe first-in, first-out (FIFO) collection of objects.
- `ConcurrentStack<T>`: Represents a thread-safe last-in, first-out (LIFO) collection of objects.

### System.Collections Classes

The `System.Collections` namespace provides non-generic collection classes that store elements as objects of type `object`. It is recommended to use the generic collections from `System.Collections.Generic` or `System.Collections.Concurrent` instead of the legacy types in `System.Collections`. Some commonly used non-generic collection classes are:

- `ArrayList`: Represents an array of objects whose size can dynamically increase as required.
- `Hashtable`: Represents a collection of key/value pairs organized based on the hash code of the key.
- `Queue`: Represents a first-in, first-out (FIFO) collection of objects.
- `Stack`: Represents a last-in, first-out (LIFO) collection of objects.

## Implementing a Collection of Key/Value Pairs

The `Dictionary<TKey, TValue>` class represents a collection of key/value pairs that are organized based on the key. Each item added to the dictionary consists of a value and its associated key. You can quickly retrieve a value by using its key. Here's an example:

```csharp
private static void IterateThruDictionary()
{
    Dictionary<string, Element> elements = BuildDictionary();

    foreach (KeyValuePair<string, Element> kvp in elements)
    {
        Element theElement = kvp.Value;

        Console.WriteLine("key: " + kvp.Key);
        Console.WriteLine("values: " + theElement.Symbol + " " +
            theElement.Name + " " + theElement.AtomicNumber);
    }
}

private static Dictionary<string, Element> BuildDictionary()
{
    var elements = new Dictionary<string, Element>();

    AddToDictionary(elements, "K", "Potassium", 19);
    AddToDictionary(elements, "Ca", "Calcium", 20);
    AddToDictionary(elements, "Sc", "Scandium", 21);
    AddToDictionary(elements, "Ti", "Titanium", 22);

    return elements;
}

private static void AddToDictionary(Dictionary<string, Element> elements,
    string symbol, string name, int atomicNumber)
{
    Element theElement = new Element();

    theElement.Symbol = symbol;
    theElement.Name = name;
    theElement

.AtomicNumber = atomicNumber;

    elements.Add(key: theElement.Symbol, value: theElement);
}

public class Element
{
    public string Symbol { get; set; }
    public string Name { get; set; }
    public int AtomicNumber { get; set; }
}
```

You can also use a collection initializer to build the dictionary:

```csharp
private static Dictionary<string, Element> BuildDictionary2()
{
    return new Dictionary<string, Element>
    {
        {"K",
            new Element() { Symbol="K", Name="Potassium", AtomicNumber=19}},
        {"Ca",
            new Element() { Symbol="Ca", Name="Calcium", AtomicNumber=20}},
        {"Sc",
            new Element() { Symbol="Sc", Name="Scandium", AtomicNumber=21}},
        {"Ti",
            new Element() { Symbol="Ti", Name="Titanium", AtomicNumber=22}}
    };
}
```

You can access dictionary elements using the `ContainsKey` method or the indexer (`[]`):

```csharp
private static void FindInDictionary(string symbol)
{
    Dictionary<string, Element> elements = BuildDictionary();

    if (elements.ContainsKey(symbol) == false)
    {
        Console.WriteLine(symbol + " not found");
    }
    else
    {
        Element theElement = elements[symbol];
        Console.WriteLine("found: " + theElement.Name);
    }
}
```

Alternatively, you can use the `TryGetValue` method to find an item by key:

```csharp
private static void FindInDictionary2(string symbol)
{
    Dictionary<string, Element> elements = BuildDictionary();

    Element theElement = null;
    if (elements.TryGetValue(symbol, out theElement) == false)
        Console.WriteLine(symbol + " not found");
    else
        Console.WriteLine("found: " + theElement.Name);
}
```

## Using LINQ to Access a Collection

LINQ (Language-Integrated Query) provides powerful querying capabilities for collections. You can use LINQ to filter, order, and group elements in a collection. Here's an example that uses LINQ to query a `List<T>`:

```csharp
private static void ShowLINQ()
{
    List<Element> elements = BuildList();

    // LINQ Query.
    var subset = from theElement in elements
                 where theElement.AtomicNumber < 22
                 orderby theElement.Name
                 select theElement;

    foreach (Element theElement in subset)
    {
        Console.WriteLine(theElement.Name + " " + theElement.AtomicNumber);
    }

    // Output:
    // Calcium 20
    // Potassium 19
    // Scandium 21
}

private static List<Element> BuildList()
{
    return new List<Element>
    {
        { new Element() { Symbol="K", Name="Potassium", AtomicNumber=19}},
        { new Element() { Symbol="Ca", Name="Calcium", AtomicNumber=20}},
        { new Element() { Symbol="Sc", Name="Scandium", AtomicNumber=21}},
        { new Element() { Symbol="Ti", Name="Titanium", AtomicNumber=22}}
    };
}

public class Element
{
    public string Symbol { get; set; }
    public string Name { get; set; }
    public int AtomicNumber { get; set; }
}
```

## Sorting a Collection

You can sort a collection by implementing the `IComparable<T>` interface in the element class. The `IComparable<T>` interface requires implementing the `CompareTo` method, which defines the criteria for sorting. Here's an example that demonstrates sorting a list of `Car` objects:

```csharp
private static void ListCars()
{
    var cars = new List<Car>
    {
        { new Car() { Name = "car1", Color = "blue", Speed = 20}},
        { new Car() { Name = "car2", Color = "red", Speed = 50}},
        { new Car() { Name = "car3", Color = "green", Speed = 10}},
        { new Car() { Name = "car4", Color = "blue", Speed = 50}},
        { new Car() { Name = "car5", Color = "blue", Speed = 30}},
        { new Car() { Name = "car6", Color = "red", Speed = 60}},
        { new Car() { Name = "car7", Color = "green", Speed = 50}}
    };

    // Sort the cars by color alphabetically and speed in descending order.
    cars.Sort();

    // View all of the cars.
    foreach (Car thisCar in cars)
    {
        Console.Write(thisCar.Color.PadRight(5) + " ");
        Console.Write(thisCar.Speed.ToString() + " ");
        Console.Write(thisCar.Name);
        Console.WriteLine();
    }

    // Output:
    // blue  50 car4
    // blue  30 car5
    // blue  20 car1
    // green 50 car7
    // green 10 car3
    // red   60 car6
    // red   50 car2
}

public class Car : IComparable<Car>
{
    public string Name { get; set; }
    public int Speed { get; set; }
    public string Color { get; set; }

    public int CompareTo(Car other)
    {
        // Compare the colors.
        int compare = String.Compare(this.Color, other.Color, true);

        // If the colors are the same, compare the speeds.
        if (compare == 0)
        {
            compare = this.Speed.CompareTo(other.Speed);

            // Use descending order for speed.
            compare = -compare;
        }

        return compare;
    }
}
```

## Defining a Custom Collection

You can define your own collection by implementing the `IEnumerable<T>` or `IEnumerable` interface. However, it's usually better to use the existing collections provided by .NET. Here's an example of defining a custom collection class named `AllColors`:

```csharp
private static void ListColors()
{
    var colors = new AllColors();

    foreach (Color theColor in colors)
    {
        Console.Write(theColor.Name + " ");
    }
    Console.WriteLine();
    // Output: red blue green
}

// Collection class.
public class AllColors : System.Collections.IEnumerable
{
    Color[] _colors =
    {
        new Color() { Name = "red" },
        new Color() { Name = "blue" },
        new Color() { Name = "green" }
    };

    public System.Collections.IEnumerator GetEnumerator()
    {
        return new ColorEnumerator(_colors);
    }

    // Custom enumerator.
    private class ColorEnumerator : System.Collections.IEnumerator
    {
        private Color[] _colors;
        private int _position = -1;

        public ColorEnumerator(Color[] colors)
        {
            _colors = colors;
        }

        object System.Collections.IEnumerator.Current
        {
            get
            {
                return _colors[_position];
            }
        }

        bool System.Collections.IEnumerator.MoveNext()
        {
            _position++;
            return (_position < _colors.Length);
        }

        void System.Collections.IEnumerator.Reset()
        {
            _position = -1;
        }
    }
}

// Element class.
public class Color
{
    public string Name { get; set

; }
}
```

## Iterators

In C#, you can use iterators to perform a custom iteration over a collection. An iterator can be a method or a get accessor that uses the `yield return` statement to return each element of the collection one at a time. Here's an example of using an iterator method to generate an even number sequence:

```csharp
private static void ListEvenNumbers()
{
    foreach (int number in EvenSequence(5, 18))
    {
        Console.Write(number.ToString() + " ");
    }
    Console.WriteLine();
    // Output: 6 8 10 12 14 16 18
}

private static IEnumerable<int> EvenSequence(int firstNumber, int lastNumber)
{
    for (var number = firstNumber; number <= lastNumber; number++)
    {
        if (number % 2 == 0)
        {
            yield return number;
        }
    }
}
```

I hope this helps! Let me know if you have any further questions.

Sure! Here are the markdown notes for the text above:

---

## Enumeration types (C# reference)

An enumeration type (or enum type) is a value type defined by a set of named constants of the underlying integral numeric type. To define an enumeration type, use the `enum` keyword and specify the names of enum members:

```csharp
enum Season
{
    Spring,
    Summer,
    Autumn,
    Winter
}
```

By default, the associated constant values of enum members are of type `int`. You can explicitly specify any other integral numeric type as the underlying type of an enumeration type. You can also explicitly specify the associated constant values.

Enumeration types can represent a choice from a set of mutually exclusive values or a combination of choices. To represent a combination of choices, define an enumeration type as bit flags.

### Enumeration types as bit flags

If you want an enumeration type to represent a combination of choices, define enum members for those choices such that an individual choice is a bit field. To indicate that an enumeration type declares bit fields, apply the `[Flags]` attribute to it.

```csharp
[Flags]
public enum Days
{
    None      = 0b_0000_0000,
    Monday    = 0b_0000_0001,
    Tuesday   = 0b_0000_0010,
    Wednesday = 0b_0000_0100,
    Thursday  = 0b_0000_1000,
    Friday    = 0b_0001_0000,
    Saturday  = 0b_0010_0000,
    Sunday    = 0b_0100_0000,
    Weekend   = Saturday | Sunday
}
```

You can use the bitwise logical operators (`|` or `&`) to combine or intersect choices represented by bit flags.

### The `System.Enum` type and enum constraint

The `System.Enum` type is the abstract base class of all enumeration types. It provides methods to get information about an enumeration type and its values. You can use `System.Enum` in a base class constraint to specify that a type parameter is an enumeration type.

### Conversions

There are explicit conversions between an enumeration type and its underlying integral type. Casting an enum value to its underlying type yields the associated integral value of an enum member. Use the `Enum.IsDefined` method to check if an enumeration type contains an enum member with a specific value.

Boxing and unboxing conversions are also available between an enumeration type and the `System.Enum` type.

---

And here are the code snippets provided in the text:

```csharp
enum ErrorCode : ushort
{
    None = 0,
    Unknown = 1,
    ConnectionLost = 100,
    OutlierReading = 200
}
```

```csharp
[Flags]
public enum Days
{
    None      = 0b_0000_0000,
    Monday    = 0b_0000_0001,
    Tuesday   = 0b_0000_0010,
    Wednesday = 0b_0000_0100,
    Thursday  = 0b_0000_1000,
    Friday    = 0b_0001_0000,
    Saturday  = 0b_0010_0000,
    Sunday    = 0b_0100_0000,
    Weekend   = Saturday | Sunday
}

public class FlagsEnumExample
{
    public static void Main()
    {
        Days meetingDays = Days.Monday | Days.Wednesday | Days.Friday;
        Console.WriteLine(meetingDays);

        Days workingFromHomeDays = Days.Thursday | Days.Friday;
        Console.WriteLine($"Join a meeting by phone on {meetingDays & workingFromHomeDays}");

        bool isMeetingOnTuesday = (meetingDays & Days.Tuesday) == Days.Tuesday;
        Console.WriteLine($"Is there a meeting on Tuesday: {isMeetingOnTuesday}");

        var a = (Days)37;
        Console.WriteLine(a);
    }
}
```

```csharp
public enum Season
{
    Spring,
    Summer,
    Autumn,
    Winter
}

public class EnumConversionExample
{
    public static void Main()
    {
        Season a = Season.Autumn;
        Console.WriteLine($"Integral value of {a} is {(int)a}");

        var b = (Season)1;
        Console.WriteLine(b);

        var c = (Season)4;
        Console.WriteLine(c);
    }
}
```

I hope this helps! Let me know if you have any further questions.

