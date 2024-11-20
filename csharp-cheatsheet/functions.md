# C# Methods (Functions) Guide

## Access Levels Explained

| Access Level | Description | Example Use Case |
|-------------|-------------|-----------------|
| `public` | Accessible from anywhere | `public void SaveUser()` - External API methods |
| `private` | Only within same class | `private void ValidateData()` - Internal helpers |
| `protected` | Class and derived classes | `protected void OnChange()` - Base class methods |
| `internal` | Same project only | `internal void Configure()` - Project-wide helpers |

## Method Declaration Style Guide

| `declare`  | `return type` | `method name` | `parameters`    |
|------------|---------------|---------------|-----------------|
| public     | int          | Add           | (int a, int b)  |
| private    | void         | PrintMessage  | (string text)   |
| protected  | bool         | IsValid       | (string input)  |

Example breakdown:

```csharp
public int Calculate(int a, int b)
↓      ↓   ↓         ↓
↓      ↓   ↓         input parameters (arguments)
↓      ↓   method name
↓      return type
declares access level
```

## 1. Basic Method Syntax

### 1.1. Method Declaration
```csharp
// Basic structure:
access_modifier return_type MethodName(parameters)
{
    // Method body
    return value; // if needed
}

// Example:
public int Add(int a, int b)
{
    return a + b;
}
```

### 1.2. Void Methods
```csharp
// Methods that don't return values
public void PrintMessage(string message)
{
    Console.WriteLine(message);
}

// Calling void methods
PrintMessage("Hello!");
```

## 2. Method Parameters

### 2.1. Optional Parameters
```csharp
public void Greet(string name, string greeting = "Hello")
{
    Console.WriteLine($"{greeting}, {name}!");
}

// Can be called either way:
Greet("John");              // Uses default greeting
Greet("John", "Hi");        // Uses provided greeting
```

### 2.2. Named Parameters
```csharp
public void CreateUser(string name, int age, string email)
{
    // Method implementation
}

// Can call with named parameters in any order:
CreateUser(
    email: "john@email.com",
    name: "John",
    age: 25
);
```

### 2.3. Parameter Modifiers

```csharp
// ref - Pass by reference
public void Swap(ref int a, ref int b)
{
    int temp = a;
    a = b;
    b = temp;
}

int x = 1, y = 2;
Swap(ref x, ref y);  // x becomes 2, y becomes 1

// out - Must assign value inside method
public bool TryParse(string input, out int result)
{
    return int.TryParse(input, out result);
}

int number;
if (TryParse("123", out number))
{
    Console.WriteLine(number);  // 123
}

// in - Read-only reference
public double CalculateDistance(in Point p1, in Point p2)
{
    // p1 and p2 cannot be modified
    return Math.Sqrt(Math.Pow(p2.X - p1.X, 2) + Math.Pow(p2.Y - p1.Y, 2));
}

// params - Variable number of parameters
public int Sum(params int[] numbers)
{
    return numbers.Sum();
}

// Can call with any number of arguments:
Sum(1, 2, 3);
Sum(1, 2, 3, 4, 5);
```

## 3. Return Values

### 3.1. Single Return Value
```csharp
public int Multiply(int a, int b)
{
    return a * b;
}

// Using the method
int result = Multiply(5, 3);  // result = 15
```

### 3.2. Multiple Return Values (Tuples)
```csharp
public (int Min, int Max) FindMinMax(int[] numbers)
{
    return (numbers.Min(), numbers.Max());
}

// Using the method
var (min, max) = FindMinMax(new[] { 1, 2, 3, 4, 5 });
// Or
(int min, int max) = FindMinMax(new[] { 1, 2, 3, 4, 5 });
```

## 4. Method Overloading

```csharp
public class Calculator
{
    // Different parameter types
    public int Add(int a, int b)
    {
        return a + b;
    }

    public double Add(double a, double b)
    {
        return a + b;
    }

    // Different number of parameters
    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }
}

// Usage:
var calc = new Calculator();
int sum1 = calc.Add(1, 2);        // Uses first method
double sum2 = calc.Add(1.5, 2.7); // Uses second method
int sum3 = calc.Add(1, 2, 3);     // Uses third method
```

## 5. Expression-Bodied Methods

```csharp
// Traditional method
public int Square(int number)
{
    return number * number;
}

// Expression-bodied method (same thing, shorter syntax)
public int Square(int number) => number * number;

// Works with void methods too
public void PrintSquare(int number) => Console.WriteLine(number * number);
```

## 6. Local Functions (Methods inside Methods)

```csharp
public int CalculateTotal(int[] numbers)
{
    // Local function
    int Square(int n) => n * n;

    int total = 0;
    foreach (var number in numbers)
    {
        total += Square(number);
    }
    return total;
}
```

## 7. Extension Methods

```csharp
public static class StringExtensions
{
    // Extension method for string type
    public static int WordCount(this string str)
    {
        return str.Split(new[] { ' ' }, StringSplitOptions.RemoveEmptyEntries).Length;
    }
}

// Usage:
string text = "Hello world!";
int wordCount = text.WordCount();  // 2
```

## 8. Async Methods

```csharp
public async Task<string> GetDataAsync()
{
    // Simulating API call
    await Task.Delay(1000);  // Wait 1 second
    return "Data";
}

// Usage:
public async Task ProcessDataAsync()
{
    string data = await GetDataAsync();
    Console.WriteLine(data);
}
```

## 9. Best Practices

### 9.1. Naming Conventions
```csharp
// Use PascalCase for method names
public void CalculateTotal() { }

// Use descriptive, action-based names
public void SendEmail() { }        // Good
public void EmailStuff() { }       // Bad

// Prefix boolean methods with question words
public bool IsValid() { }
public bool HasPermission() { }
```

### 9.2. Method Design
```csharp
// Single Responsibility Principle
public void SendEmail(string to, string subject, string body)
{
    ValidateEmail(to);
    FormatEmail(subject, body);
    DeliverEmail(to, subject, body);
}

// Keep methods small and focused
public void ProcessOrder(Order order)
{
    ValidateOrder(order);
    CalculateTotal(order);
    SaveOrder(order);
    NotifyCustomer(order);
}
```

## Detailed Explanation of Method Syntax for Beginners

### General Syntax
Every method in C# follows a standard structure:
```csharp
access_modifier return_type MethodName(parameters)
{
    // Method body
    return value; // Only if the return_type is not void
}
```

### Components Explained
1. **`access_modifier`**:
   Determines who can call the method. Common modifiers include:
   - `public`: The method is accessible from any other code.
   - `private`: The method is only accessible within the same class.
   - `protected`: Accessible within the class and any derived classes.
   - `internal`: Accessible only within the same project/assembly.

2. **`return_type`**:
   Defines what kind of data the method will return. 
   - Example: `int` means the method will return an integer.
   - Use `void` if the method does not return a value. Think of `void` as a one-way action like printing something to the console.

3. **`MethodName`**:
   - Follows PascalCase convention.
   - Should clearly describe what the method does, e.g., `CalculateSum`.

4. **`parameters`**:
   - Data inputs for the method, specified as `(type name)`.
   - Parameters are optional, but if included, they must be provided when calling the method.

### Common Beginner Mistakes
- Forgetting to use `return` in methods with non-void `return_type`.
- Using mismatched parameter types when calling a method.
- Not assigning `out` parameters inside the method.

## Real-World Example
Here's an example of a small class using methods together:
```csharp
public class ShoppingCart
{
    private List<int> items = new List<int>();

    // Add an item to the cart
    public void AddItem(int itemId)
    {
        items.Add(itemId);
    }

    // Calculate total price of items
    public double CalculateTotal()
    {
        return items.Count * 10.99; // Example pricing logic
    }

    // Print a receipt
    public void PrintReceipt()
    {
        Console.WriteLine("Receipt:");
        foreach (var item in items)
        {
            Console.WriteLine($"- Item {item}");
        }
        Console.WriteLine($"Total: {CalculateTotal():C}");
    }
}

// Example usage
ShoppingCart cart = new ShoppingCart();
cart.AddItem(101);
cart.AddItem(102);
cart.PrintReceipt();
```

## Additional Notes on Parameters
### Passing Data to Methods
- **Value Types**: Default behavior, copies the value into the method.
- **Reference Types**: The method operates on the same instance.
- **Using Modifiers**:
  - `ref`: Allows modifying the original value.
  - `out`: Requires assignment inside the method.
  - `in`: Makes the parameter read-only.

### Avoiding Parameter Overload
To keep method calls simple, consider limiting the number of parameters. If many are needed, group related ones into a class or struct.

## Why and When to Use Local Functions
Local functions are especially useful for breaking down complex logic within a method while keeping related code together. Use them to:
- Improve readability.
- Avoid cluttering the class with methods that are only relevant to one method.

```csharp
public int ComputeScore(int baseScore)
{
    int Bonus(int level) => level * 10;

    int level = 5; // Example level calculation
    return baseScore + Bonus(level);
}
```

## Best Practices Expanded
- Keep your methods **small and focused**: Each method should do one thing well.
- Use meaningful names: `CalculateTotalPrice` is better than `Calc`.
- Write comments sparingly: Explain *why*, not *what*, unless the logic is complex.
