## Typescript

- `Static Checking`: Checks error in our code without running it.
- `Type Checking`: checks if type match with type value.
- `Type Inference`: Refers to Typescripts's ability to infer type of certain values in your code.

## Differences Between Interfaces and Type Aliases in TypeScript

**Interface**:
```typescript
interface Person {
name: string;
age: number;
}
```
**type alias**:

```ts
type Person = {
  name: string;
  age: number;
};
```

### Extensibility

```ts

interface Person {
  name: string;
  age: number;
}

interface Employee extends Person {
  salary: number;
}
```

```ts
type Person = {
  name: string;
  age: number;
};

type Employee = Person & {
  salary: number;
};
```

### Declaration Merging

```ts
interface Person {
  name: string;
}

interface Person {
  age: number;
}

const person: Person = { name: "John", age: 30 }; // Valid
```
```ts
type Person = {
  name: string;
};

// Error: Duplicate identifier
type Person = {
  age: number;
};
```

| Feature                     | Interface            | Type Alias            |
|-----------------------------|----------------------|-----------------------|
| **Syntax**                  | `interface Person { name: string; age: number; }` | `type Person = { name: string; age: number; };` |
| **Extensibility**           | Can use `extends` to inherit properties. | Can use intersections (`&`) for type composition. |
| **Declaration Merging**     | Supports merging multiple declarations. | Does not support merging. |
| **Union/Primitive Types**   | Not supported.       | Supported (e.g., `type ID = string` | number;`). |
| **Use in Classes**          | Can be implemented in classes using `implements`. | Not directly implemented, but can describe shapes indirectly. |
| **Flexibility**             | Limited to object shapes and contracts. | Broad; supports unions, tuples, primitives, etc. |
| **Preferred Use Case**      | Object shapes and contracts, especially with APIs and libraries. | Complex types like unions, tuples, or mapped types. |
