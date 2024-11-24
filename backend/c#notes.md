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

### Basics of C#
- Statically Typed Programming Language i.e. variable of 1 type cannot be assigned to variable of another type.

### Namespace
- Collection of programs and libraries
- For example, the System namespace contains many types, such as the Console class referenced in the program, and many other namespaces, such as IO and Collections. 
- A <mark>using</mark> directive that references a given namespace enables unqualified use of the types that are members of that namespace. Because of the using directive, the program can use `Console.WriteLine` as shorthand for `System.Console.WriteLine`
- Declares a scope that contains a set of related types
- Type not placed in any namespace belongs to the global namespace
- Namespaces names should follow the folder structure
- Classes using same namespaces do not need to use 'using' directive to import namespaces

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

### Constructors & Object Initializers
| Constructors | Object Initializers |
| ------------ | ------------------- |
| All variables need to be passed while creating object | Preferred when all variables are not to be passed |
| Preferred when num of parameters are less | Preferred when num of parameters are more |
| Parameters are not very clear when large in number | Properties names are clear |

### init
`init` is used to set the value of property only at the time of object initialization. If we try to reset property later, we will get error. Its way of making property as private.
```c#
public class Person
{
    public string? Name { get; set; }
    public int Age { get; init; }
}
```

```c#
Person person1 = new Person
{
    Name = "Tajinder Singh",
    Age = 29
};

person1.Age = 30; // this will give error as Age cannot be set after initialization
```

### Stateless vs Stateful Class
| Stateless Class | Stateful Class |
| --------------- | -------------- |
| Maintains state of an onject of class | Do not have any state |
| Has variables and properties to maintain state | Does not have any variable or property to maintain state |


### Static class
- Static class is a stateless class
- Does not have variables or properties to maintain state
- Serves as a container for methods/ functions
- Cannot be instantiated (No object can be formed of static class)
- It can only have static methods

### Non Static Class
- Can have variables and properties
- Can have both static and non static methods

### Static Methods
- Belong to class as a whole and not to instance of a class
- Do not have access to variables and properties of a class
- cannot be called using object, but called using class
- Works faster than non static methods
- `:Thumb Rule` <mark>If a private method does not use instance (object) data, make it static<mark/>

### Non Static Method
- Cannot be called from static method
- can only be called using instance (object) of a class

### Static fiels or properties
- not a good practice to declare static fieldsa and properties
- it adds complexity to code

### const field
- const fields are implicitly static
- to be called same as stattic classes outside the class

### Best practices
- Public methods should precede the private methods in a class

### Principles
- SOLID
    - `SRP`: Single Responsibility Principles
    - `Open/Closed Principle (OCP)`: A class should be open for extension, but closed for modification. You should be able to add new functionality without changing existing code.
    - `Liskov Substitution Principle (LSP)`: Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.
    - `Interface Segregation Principle (ISP)`: Clients should not be forced to depend on interfaces they do not use. Instead of one large interface, break it into smaller, more specific interfaces.
    - `Dependency Inversion Principle (DIP)`: High-level modules should not depend on low-level modules. Both should depend on abstractions. Also, abstractions should not depend on details; details should depend on abstractions.
- DRY: Don't Repeat Yourself
- KISS: Keep it Somple, Stupid!

### Magic Number Pattern

### enum
In C#, an enum (short for enumeration) is a distinct value type that defines a set of named constants. It provides a way to represent a collection of related constants, making the code more readable and manageable. Enums are often used to represent things like days of the week, months, status codes, or any set of predefined values.

<mark>Under the hood, constants in enum have int values starting from 0 unless changed<marl/>

`Syntax:`
```C#
public enum EnumName
{
    Value1,
    Value2,
    Value3,
    // ...
}
```

`examples`
```C#
public enum DayOfWeek
{
    Sunday,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
}

public enum DayOfWeek
{
    Loss,
    Victory,
    Draw
}

public enum HttpCode
{
    Ok = 200,
    Create = 201,
    Unauthorized = 401,
    Forbidden = 403,
    Internal Server Error = 500
}
```

### Access Modifiers
- Public:
- Private:
- Protected: Can be used in dervied classes but not in other classes

### Virtual Methods
- Virtual methods or properties may be overridden in the derived classes.

### Type Casting
#### Upcasting
- Conversion of derived class to base class.
- Done by Implicit Conversion.
- Because object of derived class is also an object of base class<br>
` Ingredient ingredient = new Cheese();`

#### Downcasting
- Conversion of base class to dervied class.
- Done by Explicit Conversion.
- <mark>Must be careful</mark> because variable of base class might not be of dervied class type<br>
` Cheese chhedar = (Cheese) new Ingredient();`

```c#
public class MainClass
{
    public static void  Main(string[] args)
    {
        var ingredient = new Ingredient();
        var cheese = new Cheese();
        var cheddar = new Cheddar();

        Cheddar cheddar1= (Cheddar) cheddar.GenerateRandomIngredient();
    }
}

public class Ingredient
    {
        public Ingredient()
        {
            Console.WriteLine("class ingredient");
        }

        public Ingredient GenerateRandomIngredient()
        {
            int randomNum = new Random().Next(0, 3);
            Console.WriteLine("random number: " + randomNum);
            if (randomNum == 0) { return new Cheddar(); }
            if (randomNum == 1) { return new Mozerrela(); }
            else { return new Veggie(); }
        }
    }

    public class Cheese : Ingredient
    {
        public Cheese()
        {
            Console.WriteLine("class cheese");
        }
    }

    public class Veggie : Ingredient
    {
        public Veggie()
        {
            Console.WriteLine("class veggie");
        }
    }
```

#### 'as' operator
- used for explicit Conversion
- returns null if conversion fails
```c#
Ingredient ingredient = GenerateRandomIngredient();
Cheese chhedar = ingredient as Cheese;
if(cheddar is not null)
{
    Console.WriteLine("use cheddar");
}
else
{
    Console.WriteLine("conversion failed);
}
```

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

### Abstract Classes
- Used for classes which are not concrete
- Abstract class cannot be instantiated (cannot have object in another class)

### Abstract Methods
- Can only be added in abstract classes
- Abstract methods are implicitly virtual.
- They are only declared in base class but does not have implementation.
- They  must be overridden & implemented in derived classes.
- Their implementation can only be skipped in base classes if derived class is abstract in itself.

### Virtual vs Abstract Modifiers
| Virtual | Abstract |
| ----------- | ----------- |
| Must have an implementation | Cannot have an implementation |
| Overriding it is optional | Overriding it is mandatory |

### Extension Methods
- Extension methods can only be created in static classes
- Extension method in itself should be static method
- Extension method are useful to add methods to types we do not have access to like string class.
- Extension method are useful to add methods to types which cannot have methods defined like enums.
- Enable us to add more methods without creating a new derived type or modifying original type
- They are staic methods but can be called as we call methods on instance (object) of the type.

