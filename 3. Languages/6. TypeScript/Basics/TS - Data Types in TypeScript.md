See:
* [[TS - Introduction to TypeScript]]
* [[TS - Fundamentals of TypeScript]]
Resources:
* [Documentation: TypeScript](https://www.typescriptlang.org/)

---

# Fundamentals of Data Types
* TypeScript data types can be ***inferred*** or ***annotated**
	* Inferred Types
		* TypeScript automatically deduces the type based on the assigned value.
	* Annotated Types
		* TypeScript automatically determines the type of a variable based on the assigned value.
```TS
let age1 = 25; // TypeScript infers the type as `number`
let age2: number = 25; // Type is explicitly annotated as `number`
```
* TypeScript does not perform type coercion (e.g., it will not automatically convert string variables containing digits into numbers
```TS
let a = 12
let b = '6'

// ERROR: b is of type string, which cannot be divided by a number
console.log(a / b) 
```


---

# Data Types
* The basic data types in TypeScript:
	* ***Number***: Numeric data, including integers and floating-point numbers.
	* ***String***: Textual data
	* ***Boolean***: True/False values
	* ***Null***: The null value
	* ***Undefined***: The undefined value
	* ***BigInt***: Arbitrary-precision integers (ES2020+)
	* ***Symbol***: Unique and immutable value.
* The complex data types in TypeScript:
	* ***Object***: Any non-primitive type
	* ***Array***: Homogenous collections
	* ***Tuple***: Fixed length arrays with known types
* The special types in TypeScript:
	* ***Any***: Any type (opt-out of type checking)
	* ***Unknown***: A safer alternative to any (requires type checking before use)
	* ***Never***: Represents values that never occur (e.g., errors or infinite loops).
	* ***Void***: Represents no value (used mainly for functions with no return).
* The TypeScript-specific Constructs
	* ***Enum***: Variables that can hold multiple types
	* ***Union***: Combine multiple types into one
	* ***Intersection***: Define named constants
* The advanced data types in TypeScript
	* ***Literal Types***: Specific string, number, or boolean values.
	* ***Type Aliases***: Custom types
	* ***Interfaces***: Define object shapes


---

# Basic Data Types

## Number Type
* Numeric data, including integers and floating-point numbers.
```TS
let age: number = 25;

// The underscore can be used as a comma in TS
let sales: number = 123_456_789; 
```
## String Type
* Textual data
```TS
let course: string = "TypeScript";
let name: string = "Alice";
```
## Boolean Type
* True/false values
```TS
let isPublished: boolean = true;
let isLoggedIn: boolean = false;
```
## Null Type
* The `null` value
```TS
let data: null = null;
```
## Undefined Type
* The `undefined` value
```TS
let value: undefined = undefined;
```
## BigInt Type
* Arbitrary-precision integers (ES2020+)
```TS
let big: bigint = 9007199254740991n;
```
## Symbol
* Unique and immutable value
```TS
let sym: symbol = Symbol("unique");
```


---

# Complex Data Types
## Objects
* Any non-primitive type, which includes objects and arrays
```TS
let user: object = { id: 1, name: "Alice" };
```

```TS
// Proving that arrays are objects!
let myObject: object;

// Arrays are a type of object in JavaScript/TypeScript
myObject = [];
console.log(typeof myObject);

// This is a more conventional object in JavaScript/TypeScript.
myObject = {};
console.log(typeof myObject);
```

* TypeScript can infer the data type of objects when not specified
```TS
// TS infers that 'exampleObj' is an object where prop1 is a string and prop2 is a boolean
const exampleObj = {
	prop1: "Dave",
	prop2: true,
};

exampleObj.prop2 = 42; // ERROR -- prop2 must be a boolean
exampleObj.prop2 = false; // VALID -- prop1 is changing to a boolean
```

* Property types for an object can be defined when the object is created.
```TS
let employee: {
	id: number,
	name: string,
	retire: (date: Date) => void
} = { 
	id: 1, 
	name: 'Mosh', 
	retire: (date: Date) => {
		console.log(date)
	} 
};
```

* The data type for key-value pairs can be defined when the object is created
```TS
let chars: { [key: string]: number } = {
	"a": 1,
	"b": 2,
	"c": 3
};
```

* **Read-Only Modifiers** -- Object properties can be defined as 'read-only' to prevent them from being accessed and changed.
* **Optional Modifiers** -- Object properties can be defined as 'optional' (using a `?`) to prevent them from being mandatory
```TS
let employee: {
	readonly id: number, // creating a read-only property
	name?: string // creating an optional property
} = { id: 1, name = 'Mosh' };
```

## Arrays
- Arrays can contain items of various types.
```TS
let numbers: number[] = [1, 2, 3];
```

* TypeScript can infer the data type of arrays when not specified
```TS
// TS infers `test` as an array of `any` type because it is empty.
let test = [];
test.push("string");
test.push(42);     
test.push(true);   

// TS infers the type as `string[]` based on the initial values.
let stringArr = ["one", "hey", "Dave"]; 
stringArr[0] = "John";
stringArr.push("hey");

// TS infers the type as an array containing `string | number`.
let guitars = ["Strat", "Les Paul", 5150]; 
guitars[0] = 1984;
guitars.unshift("Jim");

// TS infers the type as a union of string, number, and boolean.
let mixedData = ["EVH", 1984, true]; 
mixedData.push(false); 
mixedData[1] = "Van Halen"; 
```

* Arrays can be assigned a type at declaration
```TS
// This array will only be able to accept string data
let bands: string[] = [];
bands.push("Kiss", "Van Halen", "Motley Crew")
```

## Tuples
* Fixed-length arrays with known types, where each element can have a different type.
```TS
let person: [string, number] = ["Alice", 25];
```

```TS
// This tuple is of type string, number and boolean, and requires 3 elements
let myTuple: [string, number, boolean] = ["Dave", 42, true];

myTuple[3] = 42 // ERROR -- there is no position #4
```

* Tuples function similarly to arrays, meaning they support all array methods.
	- The `push()` method, however, acts as a loophole, allowing you to add an item to a tuple even though its length is intended to be fixed.
```TS
// Tuples are useful when you want to define an array with a specific structure
let user: [number, string] = [1, 'Mosh']
console.log(user[1]) // Mosh
```

```TS
function displayInfo(person: [string, number]) {
    const [name, age] = person;
    console.log(`Name: ${name}, Age: ${age}`);
}

displayInfo(["Alice", 30]); // Output: Name: Alice, Age: 30
```


---

# Special Data Types

## Any Type
* Any type (opt-out of type checking).
```TS
let randomValue: any = "Hello";
randomValue = 42;
```

* This type allows any data-type to be assigned to a variable
* This type is helpful when writing code where the purpose or type of a parameter or variable is not yet determined.
```TS
// NO ERROR because album is of 'any' type
let album: any;
album = 1984
album = false
```

```ts
function render(document: any) {
	console.log(document);
}
```

## Unknown Type
* A safer alternative to `any` (requires type checking before use)
```TS
let input: unknown = "Hello";
if (typeof input === "string") {
  console.log(input.toUpperCase());
}
```

## Void Type
* Represents no value (used mainly for functions with no return).
```TS
function log(message: string): void {
  console.log(message);
}
```

## Never Type
* Represents values that never occur (e.g., errors or infinite loops).
```TS
function throwError(message: string): never {
  throw new Error(message);
}
```


---

# TypeScript-Specific Data Types

## Union Types
* Variables that can hold multiple types
```TS
let postId: string | number;
let isActive: string | boolean;

let value: string | number = "Alice"; 
value = 42;
```

```TS
function kgToLbs(weight: number | string): number {
    if (typeof weight === 'number') {
        return weight * 2.2;  // Multiply directly if the input is a number
    } else {
        return parseFloat(weight) * 2.2;  // Convert str to num & multiply
    }
}

console.log(kgToLbs(10));
console.log(kgToLbs('10'));
```

## Intersection Types
* A variable that combines multiple types to be combined into one.
```TS
type Person = { name: string };
type Employee = { id: number };
type Staff = Person & Employee;
let staff: Staff = { name: "Alice", id: 1 };
```

* A variable of an intersection type must satisfy all the types involved in the intersection.
```TS
type Draggable = {
	drag: () => void;  // The drag method has no params & no return value
};

type Resizeable = {
	resize: () => void;  // The resize method has no params & no return value
};
};

// Combine both Draggable & Resizeable types into one using an intersection type
// The resulting type UIWidget requires both drag & resize methods.
type UIWidget = Draggable & Resizeable;

// Creating an object textBox of type UIWidget
// This obj must include both drag & resize methods, due to the UIWidget type.
let textBox: UIWidget = {
	drag: () => {},    // The 'drag' method is implemented as an empty func
	resize: () => {}   // The 'resize' method is implemented as an empty func
};
```

## Enums
* Enums (short for "enumerations") are a set of named constants that can represent a collection of related values.
### Numeric Enums
* Values automatically start at `0` and increment by `1` for each subsequent member, though you can set custom values.
```TS
enum Direction {
    Up,        // 0
    Down,      // 1
    Left,      // 2
    Right      // 3
}

let dir: Direction = Direction.Up;
console.log(dir); // Output: 0
```

* Numeric Enums can also be assigned specific values
```TS
// Define an enum called 'Size' with three named constant values
enum Size { 
    Small = 1,  // 'Small' has a value of 1
    Medium = 2, // 'Medium' has a value of 2
    Large = 3   // 'Large' has a value of 3
}

// Declare a variable 'mySize' of type 'Size' and assign it the value 'Size.Medium'
let mySize: Size = Size.Medium

// Log the value of 'mySize' to the console, which will output '2'
console.log(mySize)
```
### String Enums
* Each member of a string enum must be explicitly initialized with a string literal, making it useful for non-sequential values or descriptive names.
```TS
enum Direction { Up = "UP", Down = "DOWN", Left = "LEFT", Right = "RIGHT" }

let dir: Direction = Direction.Left;
console.log(dir); // Output: "LEFT"
```
### Heterogeneous Enums
* Enums can have a mix of string and numeric members, though this is less common and can be confusing to maintain.
```TS
enum MixedEnum { No = 0, Yes = "YES" }
```
### Const Enums
* Using `const enums` enables full inlining of the code at compile time, resulting in more efficient output.
```TS
const enum Direction { Up, Down, Left, Right}

let dir = Direction.Up; // Inlined to `0` in compiled JavaScript
```


---

# Advanced Data Types
## Literal Data Types
* **Literal types** specify exact values that a variable can hold
* They are particularly useful for restricting variables to predefined values, enhancing code predictability and type safety.
```TS
let status: "success" | "error" = "success";
```

```TS
// Quantity can ONLY be a value of 50 or 100
let quantity: 50 | 100  = 100;
```

```TS
type Quantity = 50 | 100;
let quantity: Quantity = 100;
```

```TS
type Mode = 'automatic' | 'manual';

function setMode(mode: Mode) {
    console.log(`Mode set to: ${mode}`);
}

setMode('automatic');  // valid
setMode('manual');    // valid
setMode('auto');     // Error: Argument of type '"auto"' is not assignable
```

## Type Aliases
* A **type alias** is a way to create a custom types
* Type aliases can represent primitive types, object types, function types, union types, or any combination.
```TS
type ID = string | number;
let userId: ID = 123;
```

```TS
// Type aliases use pascal case

// Creating a 'Guitarist' type, with three properties, where 'name' is a string, 'active' is an optional boolean, and 'albums' is an array made up of string or numbers
type Guitarist = {
  name: string;
  active?: boolean;
  albums: (string | number)[];
};

// Creating two objects from the Guitarist type
let evh: Guitarist = {
  name: "Eddie",
  active: false,
  albums: [1984, 5150, "OU812"],
};

let jp: Guitarist = {
  name: "Jimmy",
  albums: ["I", "II", "IV"],
};

// Passing an object into a function
const greetGuitarist = (guitarist: Guitarist) => {
  return `Hello ${guitarist.name}`;
};

console.log(greetGuitarist(jp));
```

## Interfaces
* Defines object shapes
```TS
interface User {
  id: number;
  name: string;
}

let user: User = { id: 1, name: "Alice" };
```

```TS
interface Guitarist = {
  name: string;
  active?: boolean;
  albums: (string | number)[];
};

// Creating two objects from the Guitarist type
let evh: Guitarist = {
  name: "Eddie",
  active: false,
  albums: [1984, 5150, "OU812"],
};

let jp: Guitarist = {
  name: "Jimmy",
  albums: ["I", "II", "IV"],
};
```