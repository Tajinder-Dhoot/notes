
## Collections

- Collections are types implementing interfaces that define methods for collection manupulation.

## IComparable
- `The IComparable` interface in C# is used to define a generalized comparison method for objects.
- It provides a single method, CompareTo, which is used to compare the current object with another object of the same type.

### Key Features of IComparable
- Namespace: System
- Method:
```C#
int CompareTo(object obj);
```

Generic version:
```C#
int CompareTo(T other);
```

#### The CompareTo method returns:
- Negative value: If the current object is less than the object being compared.
- Zero: If the current object is equal to the object being compared.
- Positive value: If the current object is greater than the object being compared.

### When to Use IComparable
Use IComparable in the following scenarios:

#### Sorting Custom Objects
When you need to define a natural order for objects of a custom class (e.g., sorting a list of employees by their ID or name).

#### Custom Comparisons
If objects of your class need to be compared in a way that is intrinsic to the object itself, use IComparable.

#### Collections or LINQ Operations
Many collection types, such as List<T>, use IComparable when sorting or ordering elements.

## ICollection
### Scenarios to Use ICollection

#### Abstracting Collection Types
- Use ICollection when you want to handle collections generically without committing to a specific implementation like List<T> or HashSet<T>.

```C#
void ProcessCollection(ICollection<int> collection)
{
    collection.Add(42); // Add an element
    Console.WriteLine($"Collection has {collection.Count} items.");
}
```

#### When You Need Basic Collection Functionality
- If your requirement is limited to adding, removing, or counting elements, ICollection provides enough functionality without the overhead of more specialized interfaces like IList or IDictionary.

#### For Read-Only Access
- Use ICollection<T> when you want to expose a read-only collection without allowing modifications, by setting up the collection as read-only.
