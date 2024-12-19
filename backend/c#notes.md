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
- Can have abstract and non abstract methods.

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

### Interfaces
- Every 'Type' implementing the interface must implement the methods in the Interface.
- The methods in Interfaces are explicitly virtual
- Interfaces cannot be instantiated

### Interfaces vs Abstract Classes <mark>imp<mark/>
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

## Coding Practices
### Clean Code
clean code indicator = $\frac{\text{number of WTFs}}{\text{minute}}$ <br/>
Good Quality code should be
- readable
- easy to understand
- easy to maintain
- easy to find
- not be over complicated/ tricky
- developers intentions should be clear
- dev reading code is never surprised, everything should be what it seems to be
- each piece of code has one job
- naming of variables, methods, properties, classes should be meaningful and clear

### Naming variables, Properties, Methods, Classes
- If a variable or a method requires a comment to be added, it means its name is bad.
- method names should be expressive in itself.

#### Good Names
- expressive in itself
- short and precise

#### Bad Names
- meaningless names (unclear purpose)
    - var info
- overspecific names
- Hungarian Notation (adding type as prefix to variable names, was used earlier)
    - intAge
    - strName
- similar names
- confusing names
- use of abbreviations
    - var addr, var add for "address"
- Exceptions for abbreviations
    - Exception ex
    - for int(var i = 0; i < 5; i++>)
    - int Add(int a, int b)


#### Boy Scout Rule: Always leave the code you are working on a little bit better than you found it.
- Fix bad name
- Split a large method

### Principle of least surprise
- This principle says that the code we write should behave in a way that most programmers will expect it to behave.
- In other words, the readers of the code should never be surprised by what they see.
    - The methods and classes should do what their names say.
    - They should do only this thing.
    - They should do it well.
    - They should not do anything else.

```c#
// following code does what the method name says
public static List<string> GetWordsShorterThan(int length, List<string> words)
{
    List<string> results = [];
    foreach (var word in words)
    {
        if (word.Length < length)
        {
            results.Add(word);
        }
    }
    return results;
}
```

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