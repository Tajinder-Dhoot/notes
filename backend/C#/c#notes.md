
# Features of C#

## table of Contents
1. [Setup New Project](#setup-new-project)  
2. [Concepts](#concepts)  
   - [Requirements](#requirements)  
   - [Installation](#installation) 

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
- not a good practice to declare static fields and properties
- it adds complexity to code

### const field
- const fields are implicitly static
- to be called same as static classes outside the class

### Best practices
- Public methods should precede the private methods in a class

### Principles
- SOLID
    - `SRP`: Single Responsibility Principles
    - `Open/Closed Principle (OCP)`: A class should be open for extension, but closed for modification. You should be able to add new functionality without changing existing code.
    - `Liskov Substitution Principle (LSP)`: Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.
    - `Interface Segregation Principle (ISP)`: Clients should not be forced to depend on interfaces they do not use. Instead of one large interface, break it into smaller, more specific interfaces.
    - `Dependency Inversion Principle (DIP)`: High-level modules should not depend on low-level modules. Both should depend on abstractions. Also, abstractions should not depend on details; details should depend on abstractions. In other words, dependencies of a type (such as class) should not be concrete; they should be abstractions.
- DRY: Don't Repeat Yourself
- KISS: Keep it Somple, Stupid!

### Dependency Inversion Principle vs Dependency Injection
| Dependency Inversion Principle | Dependency Injection |
| ------------------------------ | -------------------- |
| dependencies of a type (such as class) should not be concrete; they should be abstractions. | class is given the dependencies it needs, it does not create them itself. |

### Magic Number Pattern

### enum
- In C#, an enum (short for enumeration) is a distinct value type that defines a set of named constants. 
- It provides a way to represent a collection of related constants, making the code more readable and manageable. 
- Enums are often used to represent things like 
    - days of the week, 
    - months, status codes, or 
    - any set of predefined values.
- cannot have funstions/ methods
- can create extension classes to create extension methods.

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
| Bundling data with methods that operate on it in the same class | Making fields private instead of public |

### Fields & Properties
| Fields | Properties |
| ----------- | ----------- |
| Variable like | Method like |
| Single Access Modifier | Separate Access Modifiers for getter and setter |
| No separate getter and setter | getter or setter may be removed |
| Cannot be overridden in derived classes | Can be overridden in derived classes |
| Should always be private | Can safely be public |

### Abstract Classes
- Used for classes which are not concrete
- Abstract class cannot be instantiated (cannot have object in another class)
- Can have abstract and non abstract methods.
- Even though abstract classes cannot be instantiated, they can have constructors. Those constructors can be used by the derived classes.

### Virtual Methods
- Virtual methods or properties may be overridden in the derived classes.

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
- They are static methods but can be called as we call methods on instance (object) of the type.

### Interfaces
- Every 'Type' implementing the interface must implement the methods in the Interface.
- The methods in Interfaces are explicitly virtual
- Interfaces cannot be instantiated

### Interfaces vs Abstract Classes <mark>imp<mark>
| Interfaces | Abstract Class |
| ----------- | ----------- |
| Set of definitions of methods | A type existing only to be derived from |
| Does not provide any implementation of its own | Can provide implementation of its own |
| All methods must be overridden in the derived types | Only abstract methods must be overridden in derived types |
| All methods are implicitly public | Non-abstract methods can have any access modifiers |
| Methods cannot be sealed or static | Can contain sealed and static methods |
| Methods are implicitly virtual | Non-abstract methods are not implicitly virtual |
| Can only contain method or properties definitions | CAn also  have implementations, fields and constructors |
| A class can implement multiple interfaces | A class cannot inherit from multiple classes |

| Property | Interfaces | Abstract Class |
| -------- | ----------- | ----------- |
| **Abstraction over:** | behavior | alikeness |
| **Defines what an object...** | ...can do | ...is |
| **Group of types share** | ...behavior | ...general category of things |
| **Example** | bird, kite and plane fly | bird, snake and dog are animals |
| **Not sure what it...** | ...is | ...is able to do |
| **Sure what it...** | ...is able to do | ...is |
| **Part of speech**| verb | noun |

### Coupling
- Coupling is the degree of interdependence between classes, measure of how closely the classes are connected

## Design Patterns
### Template Method Design Pattern
- We define the template of some algorithm in the base class.
- Specific steps of this algorithm are implementedn derived class

## Exception Handling
### Types of errors
- Compilation errors
- Run time errors
- Logical Errors

### Throwing Exceptions
- Throw specific exception first in catch block as a best practice
- Throw generic exception at last to cover any unknown exception which could occur

## LINQ Queries
- Stands for **Language Integrated Query**
- a set of technologies based on the integration of query capabilities directly into the C# language

### Deferred Execution
- Execution of a LINQ expression is delayed until the value is actually needed.
- It allows us to work with the latest data.
- It improves performance as query is only executed only when required avoiding unnecessary execution.

## .NET under the Hood
### Boxing
- concept of casting casting simple types to objects

### Garbage Collection
- In .NET, the heaps memory management mechanism is called the Garbage Collector (GC).
- Once an `object` is no longer used, it should be removed from the computer's memory so that new objects.
- It is one of the critical components of the Common Language Runtime.
- After the Garbage Collector frees the memory occupied by unused objects, it performs memory defragmentation.
- Runs in background on its own separte thread.
- It may stop all other threads when working.
- It might cause performance challenges.

#### Memory Fragmentation
- Chunks of free memory available between memory occupied by some objects.

#### Memory De-Fragmentation
- The process of moving the objects in memory to create a bigger block of free memory


## Generic Types
### Tuples
- a set of values

```c#
// following code does not follow the "Principle of least surprise"
public void SaveUser(User user)
{
    if(user.Email != null)
    {
        _userRepository.Save(user);
    }
}

// it can be refactored to
if(IsValid(user))
{
    SaveUser(user);
}

public void IsValid(User user)
{
    return user.Email != null;
}

public void SaveUser()
{
    _userRepository.Save(user);
}

```

## Key Differences

### List vs IEnumerable
| Requirement | IEnumerable | List |
| ----------- | ---- | ----------- |
| **Deferred Execution is Needed:** | When working with LINQ queries that are executed lazily, IEnumerable allows you to defer execution until the data is actually iterated. | If simple collection operations are sufficient without LINQ's deferred execution, a List may simplify your code. |
| **Read-Only Access is Sufficient:** | If you only need to loop through a collection without modifying it, IEnumerable is a good choice. | iEnumerbale is better option for read only access. |
| **Mutability is Required:** | does not support mutability. | If you need to add, remove, or modify elements in the collection, List is the appropriate choice.|
| **Random Access by Index is Needed:** | does not support access to indices. | List supports efficient indexed access, allowing you to retrieve elements by position (list[index]). |
| **Minimize Overhead:** | IEnumerable is more lightweight than List and should be used when you don't need the features of a List like adding, removing, or indexing. | |
| **Abstraction is Required:** | If you want to decouple your code from specific collection types, exposing IEnumerable in method signatures or properties helps hide implementation details. | |
| **Working with large datasets:** | When handling large datasets, especially when fetching data from a database or reading a file, IEnumerable streams the data and avoids loading everything into memory at once. | |

#### Conclusion
| Requirement | IEnumerable | List |
| ----------- | ---- | ----------- |
| **Deferred Execution is Needed:** | &#x2714; | &#x274C; |
| **Read-Only Access is Sufficient:** | &#x2714; | &#x274C;|
| **Mutability is Required:** | &#x274C; | &#x2714; |
| **Random Access by Index is Needed:** | &#x274C; | &#x2714; |
| **Minimize Overhead:** | &#x2714; | &#x274C; |
| **Abstraction is Required:** | &#x2714; | &#x274C; |
| **Working with large datasets:** | &#x2714; | &#x274C; |

### Check if Enumerable has any element using Any() vs Count()/ LongCount()
| Features | `Any()` | `Count()/ LongCount()` |
| -------- | ----- | -------------------- |
| **Difference:** | checks if at least one element exists in the collection and stops as soon as it finds the first element. | Count() or LongCount() iterates through the entire collection to determine the total number of elements, even if you're only interested in whether it contains any elements. |

#### e.g.
```c#
class C
{
    public string M1(IEnumerable<string> list)
    {
        list.Count() ? "Not empty" : "Empty"; // do not use this

        list.LongCount() ? "Not empty" : "Empty"; // do not use this

        list.Any() ? "Not empty" : "Empty"; // use this
    }
}
```

### Check if Collection has any element using `Any()` vs `Length/ Count/ IsEmpty`
| Features | `Any()` | `Length/ Count/ IsEmpty` |
| -------- | ----- | -------------------- |
| **Difference:** | Any(), which is an extension method, uses language integrated query (LINQ). It's more efficient to rely on the collection's own properties, and it also clarifies intent. | `Any()` vs `Length/ Count/ IsEmpty` are collections own properties and intent is more clear. |

#### e.g.
```c#
class C
{
    bool HasElements(string[] strings)
    {
        return strings.Any(); // do not use this
    }

    bool HasElements(string[] strings)
    {
        return strings.Length > 0; // use this
    }

    bool HasElements(string[] strings)
    {
        return strings.Count > 0; // or use this
    }
}
```

### Abstract Class vs Interface vs Static Class

| Feature                  | Abstract Class | Interface | Static Class | Extension Class |
| ------------------------ | -------------- | --------- | ------------ | --------------- |
| **Instantiation**        | &#x274C;       | &#x274C;  | &#x274C;     | &#x274C;        |
| **Multiple Inheritance** | &#x274C;       | &#x2714;  | &#x274C;     | &#x274C;        |



### Difference Between `readonly` and `const` in C#

| Feature                     | `const`                                    | `readonly`                               |
|-----------------------------|--------------------------------------------|-----------------------------------------|
| **Value Assignment**        | Must be assigned at compile-time.          | Can be assigned at runtime.             |
| **Initialization**          | Assigned when declared in the same line.  | Assigned either at declaration or in the constructor. |
| **Scope**                   | Implicitly `static`. Accessible without an instance of the class. | Instance-specific or `static`, depending on declaration. |
| **Value Type**              | Only constant literals or compile-time values (e.g., numbers, strings, `null`). | Can hold runtime-computed values, including objects. |
| **Performance**             | Value is inlined at compile-time.          | Value is resolved at runtime.           |
| **Usage**                   | Ideal for constants whose values are known at compile time and won't change (e.g., `PI = 3.14`). | Ideal for values that might be computed at runtime or depend on the instance. |
| **Modifiers Allowed**       | Implicitly `static`, cannot be combined with other modifiers. | Can be combined with `static`.          |

### Access Modifiers and Accessibility

| Caller's Location                    | `public` | `protected internal` | `protected` | `internal` | `private protected` | `private` | `file`   |
| ------------------------------------------ |----------|--------------- |-------------|------------|----------------------|--------- |--------- |
| **Within the file**                        | &#x2714; | &#x2714;       | &#x2714;    | &#x2714;    | &#x2714;            | &#x2714; | &#x2714; |
| **Within the class**                       | &#x2714; | &#x2714;       | &#x2714;    | &#x2714;    | &#x2714;            | &#x2714; | &#x274C; |
| **Derived class (same assembly)**          | &#x2714; | &#x2714;       | &#x2714;    | &#x2714;    | &#x2714;            | &#x274C; | &#x274C; |
| **Non-derived class (same assembly)**      | &#x2714; | &#x2714;       | &#x274C;    | &#x2714;    | &#x274C;            | &#x274C; | &#x274C; |
| **Derived class (different assembly)**     | &#x2714; | &#x2714;       | &#x2714;    | &#x274C;    | &#x274C;            | &#x274C; | &#x274C; |
| **Non-derived class (different assembly)** | &#x2714; | &#x274C;       | &#x274C;    | &#x274C;    | &#x274C;            | &#x274C; | &#x274C; |

