### default keyword
- gives default value of type

e.g.

```C#
public static void Main()
{
    Console.WriteLine($"default type of int: {default(int)}"); // 0
    Console.WriteLine($"default type of float: {default(float)}"); // 0
    Console.WriteLine($"default type of double: {default(double)}"); // 0
    Console.WriteLine($"default type of decimal: {default(decimal)}"); // 0
    Console.WriteLine($"default type of long: {default(long)}"); // 0
    Console.WriteLine($"default type of char: {default(char)}"); // null
    Console.WriteLine($"default type of string: {default(string)}"); // null
    Console.WriteLine($"default type of DateTime: {default(DateTime)}"); //1/1/0001 12:00:00 AM
    Console.WriteLine($"default type of class: {default(User)}"); // null
    Console.WriteLine($"default type of List of type int: {default(List<int>)}"); // null
    Console.WriteLine($"default type of List of type string: {default(List<string>)}"); // null
    Console.WriteLine($"default type of List of type generic: {default(List<Task>)}"); // null
}
```
