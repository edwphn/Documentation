# Data Types and Basic Concepts in C#

## Overview
A comprehensive guide covering C# data types and fundamental programming concepts, including type conversion, variables, operators, and basic control structures.

## Table of Contents
1. Data Types
2. Type Conversion and Casting
3. Variables and Constants
4. Operators
5. Control Structures
6. Methods (Functions)
7. Working with Built-in Types
8. Collection Usage
9. Creating Custom Types
10. Working with Generics

---

## 1. Data Types in C#

### 1.1. Value Types
Value types store data directly in memory, usually on the stack, and are passed by value.

#### Boolean Type:
- `bool`: can hold `true` or `false`.

#### Integer Types:
- `byte` (1 byte): from 0 to 255.
- `sbyte` (1 byte): from -128 to 127.
- `short` (2 bytes): from -32,768 to 32,767.
- `ushort` (2 bytes): from 0 to 65,535.
- `int` (4 bytes): from -2,147,483,648 to 2,147,483,647.
- `uint` (4 bytes): from 0 to 4,294,967,295.
- `long` (8 bytes): from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807.
- `ulong` (8 bytes): from 0 to 18,446,744,073,709,551,615.

#### Floating-Point Types:
- `float` (4 bytes): up to 7 significant digits.
- `double` (8 bytes): up to 15-16 significant digits.
- `decimal` (16 bytes): high-precision arithmetic (28-29 digits, typically used for financial calculations).

#### Character Type:
- `char` (2 bytes): a single Unicode character.

### 1.2. Reference Types
Reference types store a reference to the object in memory, which is typically located in the heap.

#### Core Reference Types:
- `string`: a sequence of characters. Immutable type.
- `object`: the base type for all data types in C#. Any type can be cast to `object`.
- `Array`: a collection of elements of the same type (indexed collection).

### 1.3. Composite Data Types

#### Collections:
- `List<T>`: a dynamic array-based list.
- `Dictionary<TKey, TValue>`: a collection that maps keys to values.
- `HashSet<T>`: a collection of unique elements.
- `Queue<T>`: a First-In-First-Out (FIFO) collection.
- `Stack<T>`: a Last-In-First-Out (LIFO) collection.
- `LinkedList<T>`: a doubly linked list.

#### Date and Time:
- `DateTime`: represents a specific moment in time.
- `TimeSpan`: represents a time interval.

#### Special Types:
- `Tuple<T1, T2, ...>`: combines multiple values.
- `Nullable<T>`: allows value types to hold `null`.
- `Task`: represents an asynchronous operation.

### 1.4. Custom Types:
```csharp
// Enumerations
enum Days { Monday, Tuesday, Wednesday }

// Structures
struct Point {
    public int X;
    public int Y;
}

// Classes
class Person {
    public string Name;
    public int Age;
}
```

---

## 2. Type Conversion and Casting

### 2.1. Implicit Conversion
```csharp
int num = 100;
long bigNum = num;        // int -> long
float f = num;           // int -> float
double d = num;          // int -> double
```

### 2.2. Explicit Conversion (Casting)
```csharp
double d = 123.45;
int num = (int)d;        // Truncates to 123
float f = (float)d;      // Possible precision loss
```

### 2.3. Using Convert Class
```csharp
string numberStr = "123";
int number = Convert.ToInt32(numberStr);
bool boolean = Convert.ToBoolean("True");
DateTime date = Convert.ToDateTime("2024-01-01");
```

### 2.4. Parse and TryParse
```csharp
// Parse (throws exception if fails)
int number = int.Parse("123");

// TryParse (safer approach)
if (int.TryParse("123", out int result))
{
    Console.WriteLine($"Parsed: {result}");
}
```

---

## 3. Variables and Constants

### 3.1. Variable Declaration
```csharp
// Explicit typing
int age = 25;
string name = "John";

// Implicit typing with var
var count = 10;          // Compiler infers int
var text = "Hello";      // Compiler infers string
var items = new List<string>();  // Compiler infers List<string>
```

### 3.2. Constants
```csharp
// Compile-time constants
const double PI = 3.14159;
const string APP_NAME = "MyApp";

// Runtime constants
readonly DateTime startupTime = DateTime.Now;
```

---

## 4. Operators

### 4.1. Arithmetic Operators
```csharp
int a = 10, b = 3;
int sum = a + b;         // Addition: 13
int diff = a - b;        // Subtraction: 7
int product = a * b;     // Multiplication: 30
int quotient = a / b;    // Division: 3
int remainder = a % b;   // Modulus: 1

// Increment/Decrement
int x = 5;
x++;                    // Post-increment
++x;                    // Pre-increment
x--;                    // Post-decrement
--x;                    // Pre-decrement
```

### 4.2. Comparison Operators
```csharp
bool isEqual = (a == b);         // Equal to
bool notEqual = (a != b);        // Not equal to
bool greater = (a > b);          // Greater than
bool less = (a < b);             // Less than
bool greaterEqual = (a >= b);    // Greater than or equal to
bool lessEqual = (a <= b);       // Less than or equal to
```

### 4.3. Logical Operators
```csharp
bool condition1 = true, condition2 = false;
bool andResult = condition1 && condition2;  // Logical AND
bool orResult = condition1 || condition2;   // Logical OR
bool notResult = !condition1;               // Logical NOT
```

### 4.4. Null-Related Operators
```csharp
// Null conditional operator (?.)
string name = customer?.FirstName;  // Null if customer is null

// Null coalescing operator (??)
string displayName = name ?? "Unknown";  // Use "Unknown" if name is null

// Null coalescing assignment (??=)
string title ??= "Default";  // Assigns "Default" if title is null
```

---

## 5. Control Structures

### 5.1. If-Else Statements
```csharp
if (condition)
{
    // code if condition is true
}
else if (anotherCondition)
{
    // code if anotherCondition is true
}
else
{
    // code if all conditions are false
}

// Ternary operator
string status = age >= 18 ? "Adult" : "Minor";
```

### 5.2. Switch Statement
```csharp
// Traditional switch
switch (day)
{
    case DayOfWeek.Monday:
        Console.WriteLine("It's Monday");
        break;
    case DayOfWeek.Friday:
        Console.WriteLine("It's Friday");
        break;
    default:
        Console.WriteLine("It's another day");
        break;
}

// Pattern matching switch expression (C# 8.0+)
string message = day switch
{
    DayOfWeek.Monday => "Start of week",
    DayOfWeek.Friday => "End of week",
    _ => "Another day"
};
```

### 5.3. Loops
```csharp
// For loop
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);
}

// Foreach loop
foreach (var item in collection)
{
    Console.WriteLine(item);
}

// While loop
while (condition)
{
    // code
}

// Do-While loop
do
{
    // code
} while (condition);
```

---

## 6. Methods (Functions)

### 6.1. Basic Method Syntax
```csharp
// Method declaration
public int Add(int a, int b)
{
    return a + b;
}

// Void method
public void PrintMessage(string message)
{
    Console.WriteLine(message);
}
```

### 6.2. Method Parameters
```csharp
// Optional parameters
public void Greet(string name, string greeting = "Hello")
{
    Console.WriteLine($"{greeting}, {name}!");
}

// Parameter modifiers
public void Swap(ref int a, ref int b)
{
    int temp = a;
    a = b;
    b = temp;
}

// Out parameter
public bool TryParse(string input, out int result)
{
    return int.TryParse(input, out result);
}

// Params array
public int Sum(params int[] numbers)
{
    return numbers.Sum();
}
```

### 6.3. Return Values
```csharp
// Single return value
public int Multiply(int a, int b)
{
    return a * b;
}

// Multiple return values (Tuple)
public (int Min, int Max) FindMinMax(int[] numbers)
{
    return (numbers.Min(), numbers.Max());
}
```

### 6.4. Method Overloading
```csharp
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }

    public double Add(double a, double b)
    {
        return a + b;
    }
}
```

### 6.5. Expression-Bodied Methods
```csharp
public int Square(int number) => number * number;
```

### 6.6. Async Methods
```csharp
public async Task<string> GetDataAsync()
{
    await Task.Delay(1000);
    return "Data";
}
```

## 7. Working with Built-in Types

### 7.1. String Operations
```csharp
string text = "Hello World";

// Common string methods
int length = text.Length;                    // 11
string upper = text.ToUpper();               // "HELLO WORLD"
string lower = text.ToLower();               // "hello world"
bool contains = text.Contains("World");      // true
string[] parts = text.Split(' ');            // ["Hello", "World"]
string trimmed = text.Trim();                // Removes whitespace
string sub = text.Substring(0, 5);           // "Hello"
string replaced = text.Replace("World", "C#"); // "Hello C#"

// String interpolation
string name = "John";
string greeting = $"Hello, {name}!";         // "Hello, John!"

// String building
StringBuilder sb = new StringBuilder();
sb.Append("Hello");
sb.AppendLine(" World");
string result = sb.ToString();
```

### 7.2. DateTime Operations
```csharp
// Creating DateTime
DateTime now = DateTime.Now;
DateTime utcNow = DateTime.UtcNow;
DateTime today = DateTime.Today;
DateTime specific = new DateTime(2024, 1, 1);

// Manipulating dates
DateTime tomorrow = today.AddDays(1);
DateTime nextWeek = today.AddDays(7);
DateTime nextMonth = today.AddMonths(1);
DateTime nextYear = today.AddYears(1);

// Formatting
string formatted = now.ToString("yyyy-MM-dd");     // "2024-11-19"
string time = now.ToString("HH:mm:ss");           // "14:30:45"
string custom = now.ToString("MM/dd/yyyy HH:mm"); // "11/19/2024 14:30"

// Date calculations
TimeSpan duration = tomorrow - today;              // 1 day
int days = duration.Days;                          // 1
```

### 7.3. Array Operations
```csharp
// Array declaration and initialization
int[] numbers = new int[5];
int[] initialized = new int[] { 1, 2, 3, 4, 5 };
string[] names = { "John", "Jane", "Bob" };

// Array methods
Array.Sort(numbers);                  // Sort array
Array.Reverse(numbers);               // Reverse array
int index = Array.IndexOf(names, "Jane"); // Find index
Array.Resize(ref numbers, 10);        // Resize array

// Multidimensional arrays
int[,] matrix = new int[3, 3];
matrix[0, 0] = 1;                     // First element
int[,,] cubic = new int[3, 3, 3];     // 3D array

// Jagged arrays
int[][] jaggedArray = new int[3][];
jaggedArray[0] = new int[] { 1, 2, 3 };
jaggedArray[1] = new int[] { 4, 5 };
```

## 8. Collection Usage

### 8.1. List<T>
```csharp
// Creating and initializing
List<string> names = new List<string>();
List<int> numbers = new List<int> { 1, 2, 3 };

// Common operations
names.Add("John");                    // Add single item
names.AddRange(new[] { "Jane", "Bob" }); // Add multiple items
names.Insert(0, "Alice");            // Insert at index
names.Remove("John");                // Remove specific item
names.RemoveAt(0);                   // Remove at index
bool exists = names.Contains("Jane"); // Check existence
names.Sort();                        // Sort list
names.Reverse();                     // Reverse list

// LINQ operations
var filtered = names.Where(n => n.StartsWith("J"));
var ordered = names.OrderBy(n => n);
```

### 8.2. Dictionary<TKey, TValue>
```csharp
// Creating and initializing
Dictionary<string, int> ages = new Dictionary<string, int>();
Dictionary<int, string> codes = new Dictionary<int, string>()
{
    { 1, "One" },
    { 2, "Two" }
};

// Common operations
ages["John"] = 25;                   // Add or update
ages.Add("Jane", 30);                // Add new only
bool exists = ages.ContainsKey("John");
ages.Remove("John");                 // Remove entry
ages.TryGetValue("Jane", out int age); // Safe get

// Iteration
foreach (KeyValuePair<string, int> pair in ages)
{
    Console.WriteLine($"{pair.Key}: {pair.Value}");
}
```

### 8.3. HashSet<T>
```csharp
// Creating and initializing
HashSet<int> numbers = new HashSet<int>();
HashSet<string> names = new HashSet<string> { "John", "Jane" };

// Common operations
numbers.Add(1);                      // Add if not present
numbers.Remove(1);                   // Remove item
bool exists = numbers.Contains(1);    // Check existence

// Set operations
HashSet<int> set1 = new HashSet<int> { 1, 2, 3 };
HashSet<int> set2 = new HashSet<int> { 2, 3, 4 };
set1.UnionWith(set2);               // Union
set1.IntersectWith(set2);           // Intersection
set1.ExceptWith(set2);              // Difference
```

## 9. Creating Custom Types

### 9.1. Class Definition
```csharp
public class Person
{
    // Properties
    public string Name { get; set; }
    public int Age { get; private set; }
    
    // Private field
    private readonly DateTime _birthDate;
    
    // Constructor
    public Person(string name, DateTime birthDate)
    {
        Name = name;
        _birthDate = birthDate;
        CalculateAge();
    }
    
    // Methods
    private void CalculateAge()
    {
        Age = DateTime.Today.Year - _birthDate.Year;
    }
    
    // Override ToString
    public override string ToString()
    {
        return $"{Name}, Age: {Age}";
    }
}
```

### 9.2. Inheritance
```csharp
public class Employee : Person
{
    public string Department { get; set; }
    public decimal Salary { get; private set; }
    
    public Employee(string name, DateTime birthDate, string department)
        : base(name, birthDate)
    {
        Department = department;
    }
    
    public virtual void GiveRaise(decimal amount)
    {
        Salary += amount;
    }
}
```

### 9.3. Interfaces
```csharp
public interface IPayable
{
    decimal CalculatePay();
    void ProcessPayment();
}

public class Contractor : IPayable
{
    public decimal HourlyRate { get; set; }
    public int HoursWorked { get; set; }
    
    public decimal CalculatePay()
    {
        return HourlyRate * HoursWorked;
    }
    
    public void ProcessPayment()
    {
        // Implementation
    }
}
```

## 10. Working with Generics

### 10.1. Generic Classes
```csharp
public class Repository<T> where T : class
{
    private List<T> _items = new List<T>();
    
    public void Add(T item)
    {
        _items.Add(item);
    }
    
    public T GetById(int id)
    {
        // Implementation
        return _items.FirstOrDefault();
    }
    
    public IEnumerable<T> GetAll()
    {
        return _items.AsEnumerable();
    }
}
```

### 10.2. Generic Methods
```csharp
public static class Utilities
{
    public static void Swap<T>(ref T first, ref T second)
    {
        T temp = first;
        first = second;
        second = temp;
    }
    
    public static bool AreEqual<T>(T first, T second) where T : IEquatable<T>
    {
        return first.Equals(second);
    }
}
```

### 10.3. Generic Constraints
```csharp
// Class constraint
public class ClassOnly<T> where T : class { }

// Struct constraint
public class StructOnly<T> where T : struct { }

// New() constraint
public class NeedsConstructor<T> where T : new() { }

// Interface constraint
public class Repository<T> where T : IEntity { }

// Multiple constraints
public class Combined<T> where T : class, IComparable, new() { }
```

### 10.4. Generic Collections
```csharp
// Generic list
List<T> list = new List<T>();

// Generic dictionary
Dictionary<TKey, TValue> dict = new Dictionary<TKey, TValue>();

// Generic queue
Queue<T> queue = new Queue<T>();

// Generic stack
Stack<T> stack = new Stack<T>();
```

---
