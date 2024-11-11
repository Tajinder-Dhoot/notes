# Features of C#
##### Strongly Typed Language
- Every variable you declare has a type known at compile time. The compiler, or editing tools tell you if you're using that type incorrectly

# Setup New Project

### Console App

##### Create Console App

`dotnet new console -n <name-of-app>`

##### Build Console App

`dotnet build`

##### Run Console App

`dotnet run`

# Concepts

### General Structure of a C# Program

```c#
// A skeleton of a C# program
using System;

// Your program starts here:
Console.WriteLine("Hello world!");

namespace YourNamespace
{
    class YourClass
    {
    }

    struct YourStruct
    {
    }

    interface IYourInterface
    {
    }

    delegate int YourDelegate();

    enum YourEnum
    {
    }

    namespace YourNestedNamespace
    {
        struct YourStruct
        {
        }
    }
}
```
### Namespace
- Collection of programs and libraries
- For example, the System namespace contains many types, such as the Console class referenced in the program, and many other namespaces, such as IO and Collections. 
- A <mark>using</mark> directive that references a given namespace enables unqualified use of the types that are members of that namespace. Because of the using directive, the program can use `Console.WriteLine` as shorthand for `System.Console.WriteLine`

### Main 

- By convention, when there are no top-level statements, the `Main` method is the entry point of an executable program; it is where the program control starts and ends.
- <mark>In a project, only one file can have `Main` method.<mark/>
- `Main` must be declared inside a class or struct. The enclosing class can be static.
- `Main` must be static.
- `Main` can have any access modifier (except file).
- `Main` can either have a void, int, Task, or Task<int> return type.
- If and only if `Main` returns a Task or Task<int>, the declaration of Main may include the async modifier. This specifically excludes an async void Main method.
- The `Main` method can be declared with or without a string[] parameter that contains command-line arguments. When using Visual Studio to create Windows applications, you can add the parameter manually or else use the GetCommandLineArgs() method to obtain the command-line arguments. Parameters are read as zero-indexed command-line arguments. Unlike C and C++, the name of the program is not treated as the first command-line argument in the args array, but it is the first element of the GetCommandLineArgs() method.

#### The following list shows the most common Main declarations:

```c#
static void Main() { }
static int Main() { }
static void Main(string[] args) { }
static int Main(string[] args) { }
static async Task Main() { }
static async Task<int> Main() { }
static async Task Main(string[] args) { }
static async Task<int> Main(string[] args) { }
```

## Basics of OOPS

### Variables

| readonly | const |
| ----------- | ----------- |
| used when we want a field never to change after it has been set in the contructor | used for things with contant value known at compilation time |
| value might not be known at compilation time | value must be known at compilation time |
| if value is set during compiling or run time, it cannot be changed| value is already set during compilation, so cannot be reset during runtime and changed later |


### Methods vs Computed Properties

```c#
public class Rectangle
{
    private double _width;
    private double _height;

    public double Width
    {
        get { return _width; }
        set { _width = value; }
    }

    public double Height
    {
        get { return _height; }
        set { _height = value; }
    }

    // Computed field (property)
    public double Area
    {
        get { return Width * Height; }  // Computed on access
    }

    // Method
    public double CalculateArea()
    {
        return Width * Height;  // Calculate the area and return it
    }
}
```

#### Key Differences:
| Feature |	Computed Field (Property) |	Method|
| ------- | ------------------------- | ----- |
| Purpose | Provides a dynamically calculated value, often based on other fields. |	Performs an action or calculation; can also return a value. |
| Access  | Accessed like a field (via the property). | Called explicitly like a function. |
| Storage | Does not store a value; computes it on access. | May or may not store values, but typically involves more complex behavior. |
| Return Type | Returns a value directly when accessed. | Can return a value, or perform an operation. |
| Example Use Case | Calculating a value based on other properties (e.g., area of a rectangle). | Performing an operation or action (e.g., updating state, sending data). |


#### When to Use Each:
- Use `computed fields` (properties) when 
    - you need a value that is derived from other data but can be treated as if it's a simple property.
    - For example, the Area of a rectangle or the Full Name of a person.

- Use `methods` when 
    - you need to perform more complex operations, 
    - possibly involving parameters, side effects, or 
    - returning values that require explicit action (e.g., calculating a value based on complex logic, interacting with external resources, etc.).

## OOPS

### Encapsulation & Data Hiding

| Encapsulation | Data Hiding |
| ----------- | ----------- |
| Bundling data with methods that perate on it in the same class | Making fields private instead of public |

### Fields & Properties
| Fields | Properties |
| ----------- | ----------- |
| Variable like | Method like |
| Single Access Modifier | Separate Access Modifiers for gette and setter |
| No separate getter and setter | getter or setter may be removed |
| Cannot be overridden in derived classes | Can be overridden in derived classes |
| Should always be private | Can safely be public |
