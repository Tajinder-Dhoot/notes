# Basic Differences: C#, JavaScript, Java, Python

| Feature                | C#                        | JavaScript             | Java                     | Python                 |
|------------------------|---------------------------|------------------------|--------------------------|------------------------|
| **Type System**        | Strongly typed, static    | Weakly typed, dynamic  | Strongly typed, static   | Strongly typed, dynamic|
| **Paradigm**           | Object-oriented, functional | Prototype-based       | Object-oriented          | Multi-paradigm (OO, functional, procedural) |
| **Compilation**        | Compiled to IL (Intermediate Language) | Interpreted          | Compiled (JVM bytecode) | Interpreted           |
| **Syntax Style**       | Curly braces `{}`         | Curly braces `{}`      | Curly braces `{}`        | Indentation-based     |
| **Platform**           | .NET Framework/.NET Core | Web browsers, Node.js  | JVM (Java Virtual Machine)| Cross-platform        |
| **Memory Management**  | Automatic (GC)           | Automatic (GC)         | Automatic (GC)           | Automatic (GC)        |
| **Variable Declaration** | `int a = 10;`            | `let a = 10;`          | `int a = 10;`            | `a = 10`              |
| **Entry Point**        | `static void Main()`      | None (script execution)| `public static void main`| `if __name__ == "__main__":` |
| **Inheritance**        | Single inheritance with interfaces | Prototype chaining   | Single inheritance with interfaces | Multiple inheritance supported |
| **Lambdas/Functions**  | `x => x + 1`             | `(x) => x + 1`         | `(x) -> x + 1`           | `lambda x: x + 1`     |
| **Error Handling**     | `try...catch`            | `try...catch`          | `try...catch`            | `try...except`        |
| **Use Cases**          | Desktop, web, game development | Web development, scripting | Enterprise applications | Data science, scripting, web development |
| **Popularity**         | Widely used for enterprise apps and games (Unity) | Ubiquitous in web development | Popular for enterprise solutions | Growing in AI/ML and scripting |
| **Notable Frameworks** | ASP.NET, Unity           | React, Angular         | Spring                   | Django, Flask         |
| **Execution Speed**    | Fast (compiled to IL)    | Slower (interpreted)   | Fast (compiled to JVM)   | Slower (interpreted)  |
| **Development Tools**  | Visual Studio, VS Code, JetBrains Rider | VS Code, WebStorm    | Eclipse, IntelliJ IDEA   | PyCharm, VS Code      |


# Performing Same Functions in Diff Languages

| Function | C# | JavaScript | Java | Python |
| -------- | -- | ---------- | ---- | ------ |
| **Print and move to new line** | Console.WriteLine("") | console.log("") | System.out.println("") | print("/n") |
| **Print and stay in same line** | Console.Write("") | console.log("") | System.out.print("") | print("") |
| **length of array** | arr.Length | arr.length | arr.length | len(arr) |
| **forEach loop**  | `foreach (int num in arr) {}` | `arr.forEach(num => {})` | `for (int num : arr) {}`| `for num in arr:` |
| **Split a string** | `string[] result = input.Split(',');` | `const result = input.split(',');` | `String[] result = input.split(",");` | `result = input.split(',')` |
| **Convert int to String** | `string result = number.ToString();` | `const result = number.toString();` | `String result2 = Integer.toString(number);` | `result = str(number)` |
| **Convert list of strings to a String** | `string result = String.Join(", ", listOfStrings);` | `let result = listOfStrings.join(", ");` | `String result = String.join(", ", stringList);` | `result = ", ".join(string_list)` |
