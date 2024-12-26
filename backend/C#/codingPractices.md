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