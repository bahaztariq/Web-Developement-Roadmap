# 🚀 JavaScript - The Language of the Web

> JavaScript is a versatile, high-level programming language that enables interactive web pages and server-side applications.

---

## 1. Introduction

### Definition
JavaScript is a lightweight, interpreted programming language that runs in web browsers and on servers (via Node.js). It enables dynamic content, interactive features, and complex applications.

### Web Stack Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    PRESENTATION LAYER                   │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌─────────────┐    ┌──────────────┐    ┌──────────┐  │
│  │    HTML     │───▶│     CSS      │───▶│    JS    │  │
│  │  Structure  │    │   Styling    │    │Behavior  │  │
│  └─────────────┘    └──────────────┘    └──────────┘  │
│        ▲                                          │    │
│        │                                          ▼    │
│   Defines Content                        Interactivity │
│                                                        │
└────────────────────────────────────────────────────────┘
                          │
                          ▼
┌────────────────────────────────────────────────────────┐
│                  JAVASCRIPT ENGINE                     │
├────────────────────────────────────────────────────────┤
│                                                        │
│   Code ──▶ Parse ──▶ Compile ──▶ Execute ──▶ Output   │
│     │         │          │          │                  │
│     ▼         ▼          ▼          ▼                  │
│  [Source]  [AST]     [Bytecode]  [Machine Code]        │
│                                                        │
└────────────────────────────────────────────────────────┘
```

### JavaScript Execution Flow

```
┌─────────────────────────────────────────────────────────┐
│                    EVENT LOOP FLOW                      │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌──────────────┐      ┌──────────────┐                │
│  │  Call Stack  │      │   Web APIs   │                │
│  │              │      │              │                │
│  │  main()      │      │  setTimeout  │                │
│  │    │         │      │  fetch()     │                │
│  │    ▼         │      │  DOM events  │                │
│  │  console.log │      │              │                │
│  └──────┬───────┘      └──────┬───────┘                │
│         │                     │                        │
│         │                     ▼                        │
│         │            ┌──────────────┐                  │
│         │            │ Callback     │                  │
│         │            │ Queue        │                  │
│         │            └──────┬───────┘                  │
│         │                   │                          │
│         └───────────────────│ (when stack empty)       │
│                             ▼                          │
│                      ┌──────────────┐                  │
│                      │ Microtask    │                  │
│                      │ Queue        │◀── Promises      │
│                      └──────────────┘                  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Where JavaScript Runs

**Definition:** JavaScript runs in two main environments: the **browser** (where it accesses the DOM, BOM, and Web APIs like `fetch`, `localStorage`, and `setTimeout`) and **Node.js** (a server-side runtime built on Chrome's V8 engine that provides access to the file system, network, and OS). The same JavaScript syntax works in both, but the available APIs differ.

```javascript
// Browser JavaScript - runs in user's web browser
// Access to: DOM, window object, fetch API
console.log('Hello from the browser!');

// Node.js JavaScript - runs on server
// Access to: file system, HTTP server, databases
console.log('Hello from the server!');
```

### Adding JavaScript to HTML

**Definition:** JavaScript is added to HTML using the `<script>` tag. External scripts (linked via `src` attribute) are the best practice for maintainability and caching. The `defer` attribute loads the script after HTML parsing without blocking rendering. The `async` attribute loads and executes the script asynchronously, without waiting for other scripts.

```html
<!-- External file (BEST PRACTICE) -->
<script src="script.js" defer></script>

<!-- Inline script (avoid when possible) -->
<script>
    console.log('Inline script');
</script>

<!-- Module script (for ES6 modules) -->
<script type="module" src="app.js"></script>

<!-- Placement matters:
   - In <head> with defer: loads in background, executes after HTML parsed
   - Before closing </body>: executes after HTML is parsed
-->
```

**Loading Attributes:**
- `defer` - Download in background, execute after HTML parsed
- `async` - Download in background, execute immediately when ready (use for independent scripts)
- No attribute - Download and execute immediately (blocks HTML parsing)

---

## 2. Variables & Data Types

### Definition
Variables store data values. JavaScript is dynamically typed, meaning variables can hold any type and change types.

### Variable Scope Chain

**Definition:** The scope chain is the mechanism JavaScript uses to resolve variable names. When a variable is referenced, JavaScript first looks in the current (local) scope, then walks up through each enclosing scope, until it reaches the global scope. If the variable is not found anywhere in the chain, a `ReferenceError` is thrown.

```
┌─────────────────────────────────────────────────────────┐
│                  SCOPE CHAIN HIERARCHY                  │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌──────────────────────────────────────────────┐       │
│  │           GLOBAL SCOPE                       │       │
│  │  const globalVar = "accessible everywhere";  │       │
│  │                                              │       │
│  │  ┌──────────────────────────────────────┐    │       │
│  │  │        FUNCTION SCOPE                │    │       │
│  │  │  const functionVar = "in function";  │    │       │
│  │  │                                      │    │       │
│  │  │  ┌──────────────────────────────┐    │    │       │
│  │  │  │      BLOCK SCOPE             │    │    │       │
│  │  │  │  const blockVar = "in block";│    │    │       │
│  │  │  │                              │    │    │       │
│  │  │  │  ┌──────────────────┐        │    │    │       │
│  │  │  │  │  INNER BLOCK     │        │    │    │       │
│  │  │  │  └──────────────────┘        │    │    │       │
│  │  │  └──────────────────────────────┘    │    │       │
│  │  └──────────────────────────────────────┘    │       │
│  └──────────────────────────────────────────────┘       │
│                                                         │
│  Access Flow: Inner ◀── Can access ──▶ Outer            │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Variable Declarations

**Definition:** JavaScript has three ways to declare variables: `var` (function-scoped, hoisted, can be redeclared — avoid in modern code), `let` (block-scoped, not hoisted to usable state, can be reassigned), and `const` (block-scoped, must be initialized, cannot be reassigned — preferred for values that don't change). Use `const` by default, `let` when reassignment is needed.

```javascript
// var - function scoped, can be redeclared, hoisted (AVOID)
var name = 'John';
var name = 'Jane';  // Allowed but problematic

// let - block scoped, can be reassigned (USE for changing values)
let age = 25;
age = 26;  // OK
// let age = 30;  // ERROR - cannot redeclare

// const - block scoped, cannot be reassigned (USE by default)
const PI = 3.14159;
// PI = 3.14;  // ERROR - cannot reassign

// const with objects/arrays - reference cannot change, but contents can
const user = { name: 'John' };
user.name = 'Jane';  // OK - modifying property
// user = {};  // ERROR - cannot reassign reference

// Best practice: Use const by default, let when reassignment needed, never var
```

### Primitive Data Types

**Definition:** JavaScript has 7 primitive data types. Primitives are immutable and compared by value, unlike objects which are compared by reference.

| Type | Description | Example |
|------|-------------|---------|
| `string` | Textual data | `'Hello'`, `"World"` |
| `number` | Integers and floating-point numbers | `42`, `3.14`, `NaN` |
| `boolean` | Logical true/false | `true`, `false` |
| `undefined` | Variable declared but not assigned | `let x;` |
| `null` | Intentional absence of value | `let x = null;` |
| `bigint` | Integers larger than Number.MAX_SAFE_INTEGER | `9007199254740991n` |
| `symbol` | Unique identifier (often for object keys) | `Symbol('id')` |


```javascript
// String - text data
const name = 'John';
const greeting = "Hello";
const template = `Hello, ${name}`;  // Template literal (ES6)

// Number - integers and floats (no separate int/float)
const integer = 42;
const float = 3.14;
const negative = -10;
const infinity = Infinity;
const notANumber = NaN;  // Result of invalid math operation

// Boolean - true or false
const isActive = true;
const isComplete = false;

// Null - intentional absence of value
const empty = null;

// Undefined - declared but not assigned
let notAssigned;  // undefined
const explicit = undefined;

// Symbol - unique identifier (ES6)
const id = Symbol('id');
const anotherId = Symbol('id');
console.log(id === anotherId);  // false - always unique

// BigInt - large integers (ES2020)
const hugeNumber = 9007199254740991n;
const alsoHuge = BigInt(9007199254740991);
```

### Reference Types

```javascript
// Object - key-value pairs
const person = {
    firstName: 'John',
    lastName: 'Doe',
    age: 30,
    isEmployed: true,
    greet() {
        return `Hello, I'm ${this.firstName}`;
    }
};

// Array - ordered list
const fruits = ['apple', 'banana', 'orange'];
const mixed = [1, 'two', true, null, { a: 1 }];

// Function - callable object
function greet(name) {
    return `Hello, ${name}`;
}

const add = function(a, b) {
    return a + b;
};

const multiply = (a, b) => a * b;

// Date
const now = new Date();
const birthday = new Date('1990-01-15');

// RegExp - regular expressions
const pattern = /hello/i;  // case-insensitive match
const emailPattern = /^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$/;
```

### Type Checking & Conversion

**Definition:** JavaScript is dynamically typed, so type checking and conversion are important. `typeof` returns the type of a value as a string. **Implicit coercion** happens automatically (e.g., `'5' + 3 = '53'`). **Explicit conversion** uses functions like `Number()`, `String()`, `Boolean()`, `parseInt()`, and `parseFloat()`. Use `===` (strict equality) to avoid unexpected type coercion in comparisons.

```javascript
// Type checking
console.log(typeof 'hello');       // 'string'
console.log(typeof 42);            // 'number'
console.log(typeof true);          // 'boolean'
console.log(typeof {});            // 'object'
console.log(typeof []);            // 'object' (arrays are objects)
console.log(typeof null);          // 'object' (bug, but permanent)
console.log(typeof undefined);     // 'undefined'
console.log(typeof function(){});  // 'function'
console.log(typeof Symbol());      // 'symbol'
console.log(typeof 123n);          // 'bigint'

// Array checking
console.log(Array.isArray([]));    // true
console.log(Array.isArray({}));    // false

// Type conversion (coercion)
// String to Number
const num1 = Number('42');         // 42
const num2 = parseInt('42px');     // 42
const num3 = parseFloat('3.14');   // 3.14
const num4 = +'42';                // 42 (unary plus)

// Number to String
const str1 = String(42);           // '42'
const str2 = (42).toString();      // '42'
const str3 = 42 + '';              // '42' (concatenation)

// Boolean conversion
console.log(Boolean(1));           // true
console.log(Boolean(0));           // false
console.log(Boolean(''));          // false
console.log(Boolean('hello'));     // true
console.log(Boolean(null));        // false
console.log(Boolean(undefined));   // false
console.log(Boolean([]));          // true
console.log(Boolean({}));          // true

// Truthy vs Falsy
// Falsy: false, 0, '', null, undefined, NaN, 0n
// Everything else is truthy
```

---

## 3. Operators

### Definition
Operators perform operations on values and variables, returning a result. They are the building blocks for expressions and computations in JavaScript.

Operators allow you to perform arithmetic calculations, assign values, compare values, combine boolean logic, and manipulate data structures efficiently.

### Arithmetic Operators

**Definition:** Arithmetic operators perform mathematical calculations: `+` (addition or string concatenation), `-` (subtraction), `*` (multiplication), `/` (division), `%` (modulo/remainder), `**` (exponentiation, ES2016), `++` (increment), and `--` (decrement). The `+` operator is special — if either operand is a string, it performs string concatenation instead of addition.

```javascript
const a = 10;
const b = 3;

console.log(a + b);    // 13 - Addition
console.log(a - b);    // 7 - Subtraction
console.log(a * b);    // 30 - Multiplication
console.log(a / b);    // 3.333... - Division
console.log(a % b);    // 1 - Modulo (remainder)
console.log(a ** b);   // 1000 - Exponentiation (ES6)

// Increment/Decrement
let x = 5;
console.log(x++);      // 5 (returns then increments)
console.log(++x);      // 7 (increments then returns)
console.log(x--);      // 7 (returns then decrements)
console.log(--x);      // 5 (decrements then returns)
```

### Assignment Operators

**Definition:** Assignment operators assign values to variables. The basic assignment operator is `=`. Compound assignment operators combine an arithmetic or bitwise operation with assignment: `+=`, `-=`, `*=`, `/=`, `%=`, `**=`, `&&=`, `||=`, `??=`. They are shorthand for `x = x + y`, `x = x - y`, etc.

```javascript
let x = 10;

x += 5;   // x = x + 5;  // 15
x -= 3;   // x = x - 3;  // 12
x *= 2;   // x = x * 2;  // 24
x /= 4;   // x = x / 4;  // 6
x %= 4;   // x = x % 4;  // 2
x **= 3;  // x = x ** 3; // 8

// Logical assignment (ES2021)
let a = null;
a ??= 'default';  // a = a ?? 'default' // 'default'

let b = true;
b &&= false;      // b = b && false     // false

let c = false;
c ||= true;       // c = c || true      // true
```

### Comparison Operators

```javascript
// Loose equality (==) - type coercion happens
console.log(5 == '5');      // true (string converted to number)
console.log(0 == false);    // true
console.log(null == undefined); // true

// Strict equality (===) - no type coercion (ALWAYS USE THIS)
console.log(5 === '5');     // false
console.log(5 === 5);       // true
console.log(null === undefined); // false

// Inequality
console.log(5 != '5');      // false (loose)
console.log(5 !== '5');     // true (strict)

// Relational
console.log(10 > 5);        // true
console.log(10 < 5);        // false
console.log(10 >= 10);      // true
console.log(10 <= 9);       // false

// Comparing objects (compares references, not content)
const obj1 = { a: 1 };
const obj2 = { a: 1 };
const obj3 = obj1;
console.log(obj1 == obj2);  // false (different references)
console.log(obj1 === obj2); // false
console.log(obj1 === obj3); // true (same reference)
```

### Logical Operators

**Definition:** Logical operators evaluate boolean expressions: `&&` (AND — returns first falsy value or last value), `||` (OR — returns first truthy value or last value), and `!` (NOT — inverts a boolean). JavaScript uses **short-circuit evaluation**: `&&` stops at the first falsy value, `||` stops at the first truthy value. This makes them useful for conditional assignments and default values.

```javascript
// AND (&&) - both must be true
console.log(true && true);   // true
console.log(true && false);  // false
console.log(false && true);  // false (short-circuits)

// OR (||) - at least one must be true
console.log(true || false);  // true (short-circuits)
console.log(false || true);  // true
console.log(false || false); // false

// NOT (!) - inverts boolean
console.log(!true);          // false
console.log(!false);         // true
console.log(!!'hello');      // true (convert to boolean)

// Short-circuit evaluation
const user = { name: 'John' };
const userName = user && user.name;  // 'John' (or undefined if user is falsy)

const defaultValue = null || 'fallback';  // 'fallback'
const value = 'exists' || 'fallback';     // 'exists'
```

### Nullish Coalescing (??) - ES2020

**Definition:** The nullish coalescing operator (`??`) returns the right-hand operand only when the left-hand operand is `null` or `undefined`. Unlike `||`, it does NOT treat `0`, `''`, or `false` as falsy — making it ideal for providing default values when a variable might legitimately be `0` or an empty string.

```javascript
// Returns right operand if left is null or undefined (not other falsy values)
const value1 = null ?? 'default';        // 'default'
const value2 = undefined ?? 'default';   // 'default'
const value3 = 0 ?? 'default';           // 0 (not null/undefined)
const value4 = '' ?? 'default';          // '' (not null/undefined)
const value5 = false ?? 'default';       // false

// Chaining
const result = value ?? fallback1 ?? fallback2 ?? 'final';

// Difference from ||
const count = 0;
console.log(count || 10);    // 10 (0 is falsy)
console.log(count ?? 10);    // 0 (0 is not null/undefined)
```

### Optional Chaining (?.) - ES2020

**Definition:** The optional chaining operator (`?.`) allows safe access to deeply nested object properties without throwing a `TypeError` if an intermediate property is `null` or `undefined`. Instead of crashing, it short-circuits and returns `undefined`. It works with property access (`obj?.prop`), method calls (`obj?.method()`), and array indexing (`arr?.[0]`).

```javascript
// Safely access nested properties without errors
const user = {
    profile: {
        name: 'John',
        address: {
            city: 'New York'
        }
    }
};

// Without optional chaining (error prone)
// const city = user.profile.address.city;  // Error if any is undefined

// With optional chaining
const city = user?.profile?.address?.city;        // 'New York'
const zip = user?.profile?.address?.zipcode;      // undefined (no error)
const country = user?.profile?.country?.name;     // undefined

// With method calls
const result = someObject?.method?.();  // undefined if method doesn't exist

// With array access
const item = array?.[0];  // undefined if array is null/undefined

// Combining with nullish coalescing
const userCity = user?.profile?.address?.city ?? 'Unknown';
```

### Ternary Operator

**Definition:** The ternary operator (`condition ? valueIfTrue : valueIfFalse`) is a concise one-line alternative to an `if/else` statement. It evaluates a condition and returns one of two values. It is best used for simple, readable expressions — avoid nesting ternaries as they quickly become hard to read.

```javascript
// condition ? trueValue : falseValue
const age = 20;
const canVote = age >= 18 ? 'Yes' : 'No';

// Nested ternary (use sparingly - can be hard to read)
const category = age < 13 ? 'child' : age < 20 ? 'teenager' : 'adult';

// Equivalent to:
let category;
if (age < 13) {
    category = 'child';
} else if (age < 20) {
    category = 'teenager';
} else {
    category = 'adult';
}
```

### Spread & Rest Operators

**Definition:** The spread operator (`...`) expands an iterable (array, string, object) into individual elements — used to copy arrays/objects, merge them, or pass array items as function arguments. The rest operator (`...`) collects multiple function arguments into a single array — it must be the last parameter. Both use the same `...` syntax but in opposite directions.

```javascript
// SPREAD (...) - expands elements

// Array spread
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];        // [1, 2, 3, 4, 5]
const arr3 = [...arr1, ...arr2];     // Combines arrays
const copy = [...arr1];              // Shallow copy

// Object spread
const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 };      // { a: 1, b: 2, c: 3 }
const obj3 = { ...obj1, b: 5 };      // { a: 1, b: 5 } - overrides b
const objCopy = { ...obj1 };         // Shallow copy

// Function arguments
const numbers = [1, 2, 3];
const max = Math.max(...numbers);    // 3 (spreads as arguments)

// REST (...) - collects remaining elements

// Function parameters
function sum(...args) {  // Collects all arguments into array
    return args.reduce((total, num) => total + num, 0);
}
sum(1, 2, 3, 4);  // 10

// Destructuring with rest
const [first, second, ...rest] = [1, 2, 3, 4, 5];
// first = 1, second = 2, rest = [3, 4, 5]

const { name, age, ...otherProps } = { name: 'John', age: 30, city: 'NYC', job: 'Dev' };
// name = 'John', age = 30, otherProps = { city: 'NYC', job: 'Dev' }
```

---

## 4. Control Flow

### Definition
Control flow statements determine the order in which code executes based on conditions and loops. They enable programs to make decisions and repeat operations.

Control flow structures allow your code to branch based on conditions (if/else, switch) and iterate over data (loops), making programs dynamic and responsive to different inputs and states.

### If/Else Statements

**Definition:** `if/else` is the fundamental conditional control structure in JavaScript. It evaluates a boolean expression and executes one block of code if the condition is truthy, and an optional `else` block if it is falsy. `else if` chains allow testing multiple conditions in sequence. Conditions use JavaScript's truthy/falsy rules, not just strict booleans.

```javascript
const age = 18;

// Basic if
if (age >= 18) {
    console.log('Adult');
}

// If/else
if (age >= 18) {
    console.log('Adult');
} else {
    console.log('Minor');
}

// If/else if/else
if (age < 13) {
    console.log('Child');
} else if (age < 20) {
    console.log('Teenager');
} else if (age < 65) {
    console.log('Adult');
} else {
    console.log('Senior');
}

// Multiple conditions
const hasID = true;
if (age >= 18 && hasID) {
    console.log('Can enter');
}

// Truthy check
const username = 'John';
if (username) {  // Checks if truthy (not empty, null, undefined)
    console.log(`Hello ${username}`);
}
```

### Switch Statement

**Definition:** The `switch` statement evaluates an expression and matches its value against a series of `case` clauses, executing the matching block. Each `case` should end with `break` to prevent fall-through (executing subsequent cases). A `default` clause handles unmatched values. Switch is most readable when comparing a single variable against many discrete values.

```javascript
const day = 3;

switch (day) {
    case 1:
        console.log('Monday');
        break;
    case 2:
        console.log('Tuesday');
        break;
    case 3:
        console.log('Wednesday');
        break;
    case 4:
    case 5:
        console.log('Thursday or Friday');
        break;
    default:
        console.log('Weekend');
}

// Switch with strings
const fruit = 'apple';
switch (fruit) {
    case 'apple':
    case 'pear':
        console.log('Pome fruit');
        break;
    case 'peach':
    case 'plum':
        console.log('Stone fruit');
        break;
}
```

### For Loops

**Definition:** The classic `for` loop repeats a block of code a specific number of times using an initializer, condition, and increment expression (`for (let i = 0; i < n; i++)`). It gives precise control over iteration and is ideal when the number of iterations is known in advance. The `for` loop is the most versatile loop type in JavaScript.

```javascript
// Standard for loop
for (let i = 0; i < 5; i++) {
    console.log(i);  // 0, 1, 2, 3, 4
}

// Loop through array
const fruits = ['apple', 'banana', 'orange'];
for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]);
}

// Decrement
for (let i = 10; i > 0; i--) {
    console.log(i);
}

// Multiple variables
for (let i = 0, j = 10; i < j; i++, j--) {
    console.log(i, j);
}

// Break and continue
for (let i = 0; i < 10; i++) {
    if (i === 3) continue;  // Skip 3
    if (i === 7) break;     // Stop at 7
    console.log(i);         // 0, 1, 2, 4, 5, 6
}

// Nested loops with labels
outer: for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
        if (i === 1 && j === 1) break outer;  // Break outer loop
        console.log(i, j);
    }
}
```

### While & Do-While Loops

**Definition:** The `while` loop repeats a block as long as a condition is truthy, checking the condition before each iteration (may execute zero times). The `do-while` loop checks the condition after each iteration, guaranteeing the block executes at least once. Both are ideal when the number of iterations is not known in advance.

```javascript
// While loop (checks condition first)
let count = 0;
while (count < 5) {
    console.log(count);
    count++;
}

// Do-while loop (executes at least once)
let num = 5;
do {
    console.log(num);  // Runs even though condition is false
    num++;
} while (num < 5);

// While for unknown iterations
let guess;
while (guess !== 'quit') {
    guess = prompt('Enter command (quit to exit):');
    if (guess !== 'quit') {
        console.log('You entered:', guess);
    }
}
```

### For...Of Loop (ES6)

**Definition:** The `for...of` loop iterates over the values of any iterable object (arrays, strings, Maps, Sets, NodeLists, generators). Unlike `for...in`, it gives you the values directly, not the keys/indices. It is the preferred way to iterate over arrays in modern JavaScript when you don't need the index.

```javascript
// Iterate over iterable values (arrays, strings, maps, sets)
const colors = ['red', 'green', 'blue'];
for (const color of colors) {
    console.log(color);
}

// With index using entries()
for (const [index, color] of colors.entries()) {
    console.log(`${index}: ${color}`);
}

// String iteration
const message = 'Hello';
for (const char of message) {
    console.log(char);  // H, e, l, l, o
}

// Set iteration
const unique = new Set([1, 2, 3, 3, 3]);
for (const num of unique) {
    console.log(num);  // 1, 2, 3
}

// Map iteration
const map = new Map([['a', 1], ['b', 2]]);
for (const [key, value] of map) {
    console.log(key, value);
}
```

### For...In Loop

**Definition:** The `for...in` loop iterates over all enumerable property keys of an object (including inherited ones from the prototype chain). It is designed for objects, not arrays — use `for...of` or `forEach` for arrays. Use `hasOwnProperty()` or `Object.keys()` to filter out inherited properties when using `for...in`.

```javascript
// Iterate over enumerable property keys (objects)
const person = {
    name: 'John',
    age: 30,
    city: 'New York'
};

for (const key in person) {
    console.log(`${key}: ${person[key]}`);
}

// Check own property (not inherited)
for (const key in person) {
    if (person.hasOwnProperty(key)) {
        console.log(key);
    }
}

// NOT recommended for arrays (iterates indices as strings)
const arr = ['a', 'b', 'c'];
for (const index in arr) {
    console.log(index, arr[index]);  // Use for...of or forEach instead
}
```

---

## 5. Functions

### Definition
Functions are reusable blocks of code that perform specific tasks. They can accept inputs (parameters) and return outputs, enabling modular and maintainable code.

Functions are first-class citizens in JavaScript, meaning they can be assigned to variables, passed as arguments, and returned from other functions. This enables powerful patterns like callbacks and higher-order functions.

### Closure Concept

**Definition:** A closure is the combination of a function and the lexical environment (scope) in which it was defined. Closures allow inner functions to access variables from their outer function's scope even after the outer function has returned. They are fundamental to JavaScript — enabling data encapsulation, factory functions, memoization, and the module pattern.

```
┌─────────────────────────────────────────────────────────┐
│                    CLOSURE CONCEPT                      │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  function outer() {                                    │
│      let count = 0;  ◀──┐  Enclosed Variable           │
│                          │  (Lexical Environment)       │
│      return {            │                              │
│          increment() {   │                              │
│              count++;    │  Access to outer scope       │
│              return count;                               │
│          }               │                              │
│      };                  │                              │
│  }                       │                              │
│                                                         │
│  const counter = outer();                              │
│                                                         │
│  counter.increment() ──▶ count: 1                      │
│  counter.increment() ──▶ count: 2                      │
│  counter.increment() ──▶ count: 3                      │
│                                                         │
│  Each call remembers its own 'count'                   │
│  through the closure mechanism                         │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Function Declarations

**Definition:** A function declaration defines a named function using the `function` keyword. Function declarations are **hoisted** — the entire function (name and body) is moved to the top of its scope, so it can be called before it appears in the code. They are the traditional way to define reusable blocks of code in JavaScript.

```javascript
// Function declaration - hoisted (can be called before definition)
function greet(name) {
    return `Hello, ${name}!`;
}
console.log(greet('John'));  // 'Hello, John!'

// With multiple parameters
function add(a, b) {
    return a + b;
}

// No parameters
function sayHello() {
    console.log('Hello!');
}

// Default return is undefined
function noReturn() {
    console.log('Doing something');
}  // Returns undefined

// Early return
function checkAge(age) {
    if (age < 0) {
        return 'Invalid age';
    }
    if (age < 18) {
        return 'Minor';
    }
    return 'Adult';
}
```

### Function Expressions

**Definition:** A function expression assigns a function to a variable. Unlike function declarations, function expressions are **not hoisted** — they cannot be called before they are defined. They can be anonymous or named, and are commonly used as callbacks, immediately invoked functions (IIFE), or when functions need to be conditionally defined.

```javascript
// Function expression - NOT hoisted
const multiply = function(a, b) {
    return a * b;
};

// Named function expression (useful for debugging)
const factorial = function fact(n) {
    if (n <= 1) return 1;
    return n * fact(n - 1);  // Can call itself by name
};

// Anonymous function (common in callbacks)
setTimeout(function() {
    console.log('Delayed message');
}, 1000);
```

### Arrow Functions (ES6)

**Definition:** Arrow functions are a concise syntax for writing function expressions using `=>`. They differ from regular functions in two key ways: they have no `this` binding (they inherit `this` from the enclosing lexical scope) and they have no `arguments` object. Arrow functions with a single expression can omit the `return` keyword and curly braces.

```javascript
// Basic arrow function
const add = (a, b) => {
    return a + b;
};

// Implicit return (single expression, no braces)
const multiply = (a, b) => a * b;
const square = x => x * x;  // Single param can omit parentheses

// Multiple statements need braces
const calculate = (a, b) => {
    const sum = a + b;
    const product = a * b;
    return { sum, product };
};

// Returning object (wrap in parentheses)
const makePerson = (name, age) => ({ name, age });

// No arguments
const getRandom = () => Math.random();

// Arrow functions don't have their own 'this' (inherits from parent)
const obj = {
    name: 'John',
    // Regular function - has its own 'this'
    sayHiRegular: function() {
        console.log('Hi, ' + this.name);
    },
    // Arrow function - 'this' is from surrounding scope
    sayHiArrow: () => {
        console.log('Hi, ' + this.name);  // 'this' is not obj
    }
};
```

### Parameters & Arguments

**Definition:** Parameters are the named variables listed in a function's definition. Arguments are the actual values passed when calling the function. JavaScript supports default parameters (ES6), rest parameters (`...args` to collect remaining arguments into an array), and destructured parameters. Extra arguments are ignored; missing ones are `undefined` unless a default is set.

```javascript
// Default parameters (ES6)
function greet(name = 'Guest', greeting = 'Hello') {
    return `${greeting}, ${name}!`;
}
greet();              // 'Hello, Guest!'
greet('John');        // 'Hello, John!'
greet('John', 'Hi');  // 'Hi, John!'

// Destructuring parameters
function displayUser({ name, age, email = 'N/A' }) {
    console.log(`${name} (${age}) - ${email}`);
}
displayUser({ name: 'John', age: 30 });  // John (30) - N/A

// Rest parameters (collects remaining args into array)
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}
sum(1, 2, 3, 4, 5);  // 15

// Mixing parameter types
function example(required, optional = 'default', ...rest) {
    console.log(required, optional, rest);
}
example('must');              // 'must', 'default', []
example('must', 'opt');       // 'must', 'opt', []
example('must', 'opt', 1, 2); // 'must', 'opt', [1, 2]

// Arguments object (old way, avoid in new code)
function oldStyle() {
    console.log(arguments);  // Array-like object with all arguments
    // Convert to array
    const args = Array.from(arguments);
}
```

### Scope & Hoisting

**Definition:** Scope determines where variables are accessible. JavaScript has global scope, function scope, and block scope (ES6+). **Hoisting** is JavaScript's behavior of moving variable and function declarations to the top of their scope before execution. `var` declarations are hoisted and initialized as `undefined`; `let`/`const` are hoisted but not initialized (Temporal Dead Zone); function declarations are fully hoisted.

```javascript
// HOISTING

// Function declarations are hoisted (moved to top)
sayHi();  // Works!
function sayHi() {
    console.log('Hi');
}

// Variable declarations are hoisted (but not initialization)
console.log(x);  // undefined (not error)
var x = 5;

// let and const are hoisted but in "temporal dead zone"
// console.log(y);  // ERROR!
let y = 10;

// SCOPE

// Global scope
const globalVar = 'I am global';

function outer() {
    // Function scope
    const outerVar = 'I am in outer';
    
    if (true) {
        // Block scope (ES6)
        const blockVar = 'I am in block';
        let blockLet = 'Me too';
        var functionVar = 'I am function scoped';
        
        console.log(globalVar);   // Accessible
        console.log(outerVar);    // Accessible
        console.log(blockVar);    // Accessible
    }
    
    // console.log(blockVar);     // ERROR - not accessible
    console.log(functionVar);     // Accessible (var is function scoped)
}

// Lexical scope (inner functions access outer variables)
function outer() {
    const outerVar = 'outer';
    
    function inner() {
        const innerVar = 'inner';
        console.log(outerVar);  // Can access outer
        console.log(innerVar);  // Can access own
    }
    
    inner();
    // console.log(innerVar);   // ERROR - not accessible
}
```

### Closures

**Definition:** A closure is a function that retains access to its outer (enclosing) function's variables even after the outer function has finished executing. This happens because JavaScript functions carry a reference to their lexical scope. Closures enable powerful patterns like data privacy (private variables), factory functions, partial application, and memoization.

```javascript
// A closure is a function that remembers its outer scope even when executed elsewhere

function createCounter() {
    let count = 0;  // Private variable
    
    return {
        increment() {
            count++;
            return count;
        },
        decrement() {
            count--;
            return count;
        },
        getCount() {
            return count;
        }
    };
}

const counter1 = createCounter();
const counter2 = createCounter();

console.log(counter1.increment());  // 1
console.log(counter1.increment());  // 2
console.log(counter2.increment());  // 1 (separate closure)

// Practical: Function factories
function makeMultiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

const double = makeMultiplier(2);
const triple = makeMultiplier(3);

console.log(double(5));   // 10
console.log(triple(5));   // 15

// Practical: Private methods
const bankAccount = (function() {
    let balance = 0;  // Private
    
    return {
        deposit(amount) {
            balance += amount;
            return balance;
        },
        withdraw(amount) {
            if (amount > balance) {
                return 'Insufficient funds';
            }
            balance -= amount;
            return balance;
        },
        getBalance() {
            return balance;
        }
    };
})();
```

### IIFE (Immediately Invoked Function Expression)

**Definition:** An IIFE is a function that is defined and immediately called in the same expression. It creates a private scope, preventing variable pollution of the global namespace. IIFEs were the primary way to create modules before ES6 modules. The pattern is `(function() { ... })()` or `(() => { ... })()`.

```javascript
// Classic IIFE pattern
(function() {
    const privateVar = 'I am private';
    console.log('IIFE executed');
})();

// With arrow function
(() => {
    console.log('Arrow IIFE');
})();

// With parameters
((name) => {
    console.log(`Hello, ${name}`);
})('World');

// Practical: Create private scope
const module = (function() {
    const privateData = [];
    
    return {
        add(item) {
            privateData.push(item);
        },
        getAll() {
            return [...privateData];
        }
    };
})();

module.add('item1');
console.log(module.getAll());  // ['item1']
// console.log(module.privateData);  // undefined - not accessible
```

### Callbacks & Higher-Order Functions

**Definition:** A **callback** is a function passed as an argument to another function, to be called later (synchronously or asynchronously). A **higher-order function** is any function that takes a function as an argument or returns a function. Higher-order functions like `map`, `filter`, `reduce`, and `forEach` are the foundation of functional programming in JavaScript.

```javascript
// Callback function - passed as argument to another function
function fetchData(callback) {
    setTimeout(() => {
        const data = { id: 1, name: 'John' };
        callback(data);
    }, 1000);
}

fetchData(function(data) {
    console.log('Received:', data);
});

// Higher-order function - takes function as argument or returns function

// Takes function as argument
function withLogging(fn) {
    return function(...args) {
        console.log('Calling function with:', args);
        const result = fn(...args);
        console.log('Result:', result);
        return result;
    };
}

const loggedAdd = withLogging((a, b) => a + b);
loggedAdd(2, 3);  // Logs: Calling..., Result: 5

// Returns function
function createGreeter(greeting) {
    return function(name) {
        return `${greeting}, ${name}!`;
    };
}

const sayHello = createGreeter('Hello');
const sayGoodbye = createGreeter('Goodbye');

console.log(sayHello('John'));     // 'Hello, John!'
console.log(sayGoodbye('Jane'));   // 'Goodbye, Jane!'

// Array methods with callbacks (common pattern)
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(n => n * 2);
const evens = numbers.filter(n => n % 2 === 0);
const sum = numbers.reduce((acc, n) => acc + n, 0);
```

### Recursion

**Definition:** Recursion is a technique where a function calls itself to solve a problem by breaking it into smaller subproblems of the same type. Every recursive function needs a **base case** (a condition that stops the recursion) and a **recursive case** (the self-call that moves toward the base case). Without a base case, recursion causes a stack overflow.

```javascript
// Function calling itself

// Factorial
function factorial(n) {
    if (n <= 1) return 1;  // Base case
    return n * factorial(n - 1);  // Recursive case
}
console.log(factorial(5));  // 120

// Fibonacci
function fibonacci(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

// Sum array
function sumArray(arr) {
    if (arr.length === 0) return 0;
    return arr[0] + sumArray(arr.slice(1));
}

// Deep object search
function findValue(obj, key) {
    if (obj.hasOwnProperty(key)) {
        return obj[key];
    }
    
    for (let prop in obj) {
        if (typeof obj[prop] === 'object' && obj[prop] !== null) {
            const result = findValue(obj[prop], key);
            if (result !== undefined) return result;
        }
    }
    return undefined;
}

// Flatten array
function flatten(arr) {
    return arr.reduce((flat, item) => {
        return flat.concat(Array.isArray(item) ? flatten(item) : item);
    }, []);
}

flatten([1, [2, [3, 4], 5], 6]);  // [1, 2, 3, 4, 5, 6]
```

---

## 6. Arrays

### Definition
Arrays are ordered collections of values that can hold any data type. They are zero-indexed and dynamic, making them ideal for storing and manipulating lists of data.

Arrays are one of JavaScript's most powerful data structures, providing built-in methods for iteration, transformation, searching, and manipulation. Understanding array methods is essential for writing clean, functional JavaScript code.

### Array Methods Flow

```
┌─────────────────────────────────────────────────────────┐
│                ARRAY METHODS PIPELINE                   │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Original Array: [1, 2, 3, 4, 5, 6]                     │
│                                                         │
│         │                                               │
│         ▼                                               │
│  ┌──────────────┐                                       │
│  │    filter()  │  (n) => n % 2 === 0                  │
│  │  [2, 4, 6]   │  Keep only even numbers              │
│  └──────┬───────┘                                       │
│         │                                               │
│         ▼                                               │
│  ┌──────────────┐                                       │
│  │     map()    │  (n) => n * 2                        │
│  │  [4, 8, 12]  │  Double each value                   │
│  └──────┬───────┘                                       │
│         │                                               │
│         ▼                                               │
│  ┌──────────────┐                                       │
│  │   reduce()   │  (acc, n) => acc + n, 0              │
│  │     24       │  Sum all values                      │
│  └──────────────┘                                       │
│                                                         │
│  Chain: array.filter().map().reduce()                   │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Creating & Accessing Arrays

**Definition:** Arrays in JavaScript are ordered, zero-indexed collections that can hold any mix of data types. They are objects with numeric keys and a `length` property. Arrays are created with array literals (`[]`) or `new Array()`. Elements are accessed by index (`arr[0]`), and arrays are dynamic — they grow and shrink automatically.

```javascript
// Creating arrays
const fruits = ['apple', 'banana', 'orange'];
const mixed = [1, 'two', true, null, { a: 1 }, [1, 2]];
const empty = [];
const withLength = new Array(3);  // [empty × 3]

// Accessing elements
console.log(fruits[0]);      // 'apple'
console.log(fruits[1]);      // 'banana'
console.log(fruits[10]);     // undefined

// Getting length
console.log(fruits.length);  // 3

// Accessing last element
const last = fruits[fruits.length - 1];  // 'orange'
const alsoLast = fruits.at(-1);          // 'orange' (ES2022)

// Modifying elements
fruits[1] = 'blueberry';
fruits[10] = 'grape';  // Creates sparse array (holes)

// Check if array
console.log(Array.isArray(fruits));  // true
console.log(Array.isArray({}));      // false
```

### Array Methods Reference

| Method | Description | Mutates Original? | Returns |
|--------|-------------|-------------------|---------|
| `push()` | Add element(s) to end | ✅ Yes | New length |
| `pop()` | Remove element from end | ✅ Yes | Removed element |
| `unshift()` | Add element(s) to start | ✅ Yes | New length |
| `shift()` | Remove element from start | ✅ Yes | Removed element |
| `splice()` | Add/remove at index | ✅ Yes | Array of removed items |
| `sort()` | Sort elements in place | ✅ Yes | Sorted array (reference) |
| `reverse()` | Reverse order in place | ✅ Yes | Reversed array (reference) |
| `slice()` | Extract portion of array | ❌ No | New array |
| `concat()` | Merge arrays | ❌ No | New merged array |
| `map()` | Transform elements | ❌ No | New transformed array |
| `filter()` | Select elements | ❌ No | New filtered array |
| `reduce()` | Accumulate to single value| ❌ No | Accumulated value |

### Mutating Methods (Modify Original Array)


```javascript
const arr = [1, 2, 3];

// push() - add to end, returns new length
arr.push(4);        // [1, 2, 3, 4]
arr.push(5, 6);     // Can add multiple

// pop() - remove from end, returns removed element
const last = arr.pop();  // 6, arr is now [1, 2, 3, 4, 5]

// unshift() - add to beginning, returns new length
arr.unshift(0);     // [0, 1, 2, 3, 4, 5]

// shift() - remove from beginning, returns removed element
const first = arr.shift();  // 0

// splice() - add/remove at specific index
// array.splice(start, deleteCount, item1, item2, ...)
const numbers = [1, 2, 3, 4, 5];

// Remove elements
const removed = numbers.splice(2, 2);  // Removes 2 elements from index 2
// numbers: [1, 2, 5], removed: [3, 4]

// Add elements
numbers.splice(1, 0, 'a', 'b');  // Insert at index 1, remove 0
// numbers: [1, 'a', 'b', 2, 5]

// Replace elements
numbers.splice(1, 2, 'x', 'y');  // Remove 2, add 2
// numbers: [1, 'x', 'y', 2, 5]

// sort() - sorts in place (converts to strings by default!)
const items = ['banana', 'apple', 'cherry'];
items.sort();  // ['apple', 'banana', 'cherry']

const nums = [10, 2, 30, 1];
nums.sort();   // [1, 10, 2, 30] - WRONG! String comparison
nums.sort((a, b) => a - b);  // [1, 2, 10, 30] - Correct numeric sort

// reverse() - reverses in place
items.reverse();  // ['cherry', 'banana', 'apple']

// fill() - fill with static value
const zeros = new Array(5).fill(0);     // [0, 0, 0, 0, 0]
zeros.fill(5, 1, 3);  // [0, 5, 5, 0, 0] - fill 5 at indices 1-2
```

### Non-Mutating Methods (Return New Array)

```javascript
const arr = [1, 2, 3, 4, 5];

// slice() - extract portion (doesn't modify original)
const sliced = arr.slice(1, 4);   // [2, 3, 4] (start inclusive, end exclusive)
const fromIndex = arr.slice(2);   // [3, 4, 5] (to end)
const copy = arr.slice();         // Shallow copy of entire array
const last3 = arr.slice(-3);      // [3, 4, 5] (negative indices)

// concat() - combine arrays
const arr1 = [1, 2];
const arr2 = [3, 4];
const combined = arr1.concat(arr2, 5, 6);  // [1, 2, 3, 4, 5, 6]

// toSorted(), toReversed(), toSpliced() (ES2023) - non-mutating versions
const original = [3, 1, 4, 1, 5];
const sorted = original.toSorted((a, b) => a - b);  // [1, 1, 3, 4, 5]
// original unchanged: [3, 1, 4, 1, 5]

// with() (ES2023) - update at index without mutating
const updated = original.with(2, 99);  // [3, 1, 99, 1, 5]
```

### Iteration Methods

```javascript
const numbers = [1, 2, 3, 4, 5];

// forEach() - execute function for each element
numbers.forEach((num, index, array) => {
    console.log(`${index}: ${num}`);
});

// map() - transform each element, return new array
const doubled = numbers.map(num => num * 2);  // [2, 4, 6, 8, 10]
const squares = numbers.map(num => ({
    value: num,
    squared: num ** 2
}));

// filter() - return elements that pass test
const evens = numbers.filter(num => num % 2 === 0);      // [2, 4]
const greaterThan3 = numbers.filter(num => num > 3);     // [4, 5]

// reduce() - reduce array to single value
const sum = numbers.reduce((acc, num) => acc + num, 0);  // 15
const product = numbers.reduce((acc, num) => acc * num, 1);  // 120
const max = numbers.reduce((max, num) => num > max ? num : max, numbers[0]);

// reduceRight() - reduce from right to left
const reversed = numbers.reduceRight((acc, num) => acc + num, '');  // '54321'

// find() - return first element that passes test
const firstEven = numbers.find(num => num % 2 === 0);    // 2
const firstLarge = numbers.find(num => num > 10);        // undefined

// findIndex() - return index of first match
const firstEvenIndex = numbers.findIndex(num => num % 2 === 0);  // 1

// findLast() / findLastIndex() (ES2023)
const lastEven = numbers.findLast(num => num % 2 === 0);  // 4

// some() - test if ANY element passes
const hasEven = numbers.some(num => num % 2 === 0);      // true
const hasNegative = numbers.some(num => num < 0);        // false

// every() - test if ALL elements pass
const allPositive = numbers.every(num => num > 0);       // true
const allEven = numbers.every(num => num % 2 === 0);     // false

// flatMap() - map then flatten one level
const sentences = ['Hello world', 'Goodbye moon'];
const words = sentences.flatMap(sentence => sentence.split(' '));  // ['Hello', 'world', 'Goodbye', 'moon']
```

### Searching Methods

```javascript
const fruits = ['apple', 'banana', 'orange', 'apple'];

// indexOf() - first occurrence, -1 if not found
console.log(fruits.indexOf('banana'));     // 1
console.log(fruits.indexOf('grape'));      // -1

// lastIndexOf() - last occurrence
console.log(fruits.lastIndexOf('apple'));  // 3

// includes() - check if contains (ES2016)
console.log(fruits.includes('banana'));    // true
console.log(fruits.includes('grape'));     // false

// find() with complex condition
const users = [
    { id: 1, name: 'John' },
    { id: 2, name: 'Jane' }
];
const user = users.find(u => u.id === 2);  // { id: 2, name: 'Jane' }
```

### Array Destructuring

**Definition:** Array destructuring is an ES6 syntax that unpacks values from an array into distinct variables in a single statement. It uses positional matching — the first variable gets the first element, the second gets the second, etc. You can skip elements with commas, set default values, and use rest syntax (`...rest`) to collect remaining elements.

```javascript
// Basic destructuring
const [first, second] = [1, 2, 3, 4];
console.log(first);   // 1
console.log(second);  // 2

// Skip elements
const [a, , c] = [1, 2, 3, 4];
console.log(a, c);    // 1, 3

// Rest pattern
const [head, ...tail] = [1, 2, 3, 4];
console.log(head);    // 1
console.log(tail);    // [2, 3, 4]

// Default values
const [x = 0, y = 0, z = 0] = [1, 2];
console.log(x, y, z); // 1, 2, 0

// Swapping variables
let m = 1, n = 2;
[m, n] = [n, m];
console.log(m, n);    // 2, 1

// Nested destructuring
const nested = [1, [2, 3], 4];
const [i, [j, k], l] = nested;
console.log(i, j, k, l);  // 1, 2, 3, 4
```

---

## 7. Objects

### Definition
Objects are collections of key-value pairs (properties). Keys are strings or symbols, values can be any type, making objects the foundation of JavaScript's object-oriented programming.

Objects allow you to group related data and functionality together. They serve as the building blocks for more complex data structures, classes, and the foundation of JavaScript's prototype-based inheritance system.

### Prototype Chain

**Definition:** The prototype chain is JavaScript's inheritance mechanism. Every object has an internal `[[Prototype]]` link pointing to another object (its prototype). When a property is accessed, JavaScript first looks on the object itself, then walks up the prototype chain until it finds the property or reaches `null`. This enables shared methods across all instances without duplicating them in memory.

```
┌─────────────────────────────────────────────────────────┐
│                  PROTOTYPE CHAIN                        │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌──────────────────────────────────────────────┐      │
│  │           Object.prototype                   │      │
│  │  • toString()                                │      │
│  │  • valueOf()                                 │      │
│  │  • hasOwnProperty()                          │      │
│  └──────────────┬───────────────────────────────┘      │
│                 │                                       │
│                 │ [[Prototype]]                         │
│                 ▼                                       │
│  ┌──────────────────────────────────────────────┐      │
│  │           Animal.prototype                   │      │
│  │  • constructor: Animal                       │      │
│  │  • speak() { return "sound"; }               │      │
│  └──────────────┬───────────────────────────────┘      │
│                 │                                       │
│                 │ [[Prototype]]                         │
│                 ▼                                       │
│  ┌──────────────────────────────────────────────┐      │
│  │              dog (instance)                  │      │
│  │  • name: "Buddy"                             │      │
│  │  • speak() ──▶ Animal.prototype.speak()     │      │
│  └──────────────────────────────────────────────┘      │
│                                                         │
│  Lookup: dog.speak() ──▶ Animal.prototype ──▶          │
│          Object.prototype ──▶ null                     │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Creating Objects

**Definition:** JavaScript objects can be created in several ways: object literals (`{}`), constructor functions (called with `new`), `Object.create()` (specifying the prototype directly), and ES6 classes (syntactic sugar over constructor functions). Object literals are the most common for simple objects; classes are preferred for creating multiple instances with shared behavior.

```javascript
// Object literal (most common)
const person = {
    firstName: 'John',
    lastName: 'Doe',
    age: 30
};

// Using new Object() (rarely used)
const obj = new Object();
obj.name = 'Jane';

// Object.create() - create with prototype
const proto = { greet() { return 'Hello'; } };
const child = Object.create(proto);
console.log(child.greet());  // 'Hello' (inherited)

// Constructor function
function Person(name, age) {
    this.name = name;
    this.age = age;
}
const john = new Person('John', 30);

// Class (ES6)
class User {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
}
const jane = new User('Jane', 25);
```

### Accessing & Modifying Properties

**Definition:** Object properties are accessed using dot notation (`obj.prop`) or bracket notation (`obj['prop']`). Bracket notation is required when the key is dynamic, contains special characters, or is a variable. Properties can be added, modified, or deleted at any time. `Object.keys()`, `Object.values()`, and `Object.entries()` provide array views of an object's enumerable properties.

```javascript
const person = {
    firstName: 'John',
    'last-name': 'Doe',  // Quoted key with special char
    age: 30
};

// Dot notation (preferred when possible)
console.log(person.firstName);   // 'John'
person.age = 31;                 // Modify

// Bracket notation (required for dynamic keys or special chars)
console.log(person['last-name']);  // 'Doe'
console.log(person['firstName']);  // 'John'

// Dynamic property access
const prop = 'firstName';
console.log(person[prop]);  // 'John'

// Property existence
console.log('age' in person);           // true
console.log(person.hasOwnProperty('age'));  // true (own property only)
console.log(person.gender !== undefined);   // false

// Adding properties
person.email = 'john@example.com';
person['phone'] = '555-1234';

// Deleting properties
delete person.phone;

// Computed property names (ES6)
const key = 'dynamicKey';
const obj = {
    [key]: 'value',
    [`${key}2`]: 'value2',
    [1 + 1]: 'four'  // Computed: 4: 'four'
};
```

### Object Methods

```javascript
const calculator = {
    value: 0,
    
    // Method shorthand (ES6)
    add(n) {
        this.value += n;
        return this;  // Enable chaining
    },
    
    subtract(n) {
        this.value -= n;
        return this;
    },
    
    multiply(n) {
        this.value *= n;
        return this;
    },
    
    getValue() {
        return this.value;
    },
    
    // Arrow function (no own 'this', inherits from parent)
    logArrow: () => {
        console.log(this.value);  // 'this' is not calculator!
    },
    
    // Regular function (has own 'this')
    logRegular() {
        console.log(this.value);  // 'this' is calculator
    }
};

// Method chaining
calculator.add(5).subtract(2).multiply(3);
console.log(calculator.getValue());  // 9
```

### The 'this' Keyword

**Definition:** `this` refers to the object that is currently executing the function. Its value depends on **how** the function is called: in a method call, `this` is the object before the dot; in a regular function, `this` is `undefined` (strict mode) or the global object; in an arrow function, `this` is inherited from the enclosing lexical scope. `call()`, `apply()`, and `bind()` explicitly set `this`.

```javascript
// 'this' depends on how function is called

// Global context (non-strict)
console.log(this);  // Window (browser) or global (Node)

// Object method
const obj = {
    name: 'Object',
    getName() {
        return this.name;  // 'this' is obj
    }
};
console.log(obj.getName());  // 'Object'

// Standalone function
function standalone() {
    console.log(this);  // Window (non-strict) or undefined (strict)
}

// Constructor function
function Person(name) {
    this.name = name;  // 'this' is new instance
}

// Event handler (browser)
// button.addEventListener('click', function() {
//     console.log(this);  // 'this' is the button element
// });

// Arrow function (inherits 'this' from parent scope)
const outer = {
    name: 'Outer',
    regularFn: function() {
        console.log(this.name);  // 'Outer'
        
        setTimeout(function() {
            console.log(this.name);  // undefined (this is window/undefined)
        }, 100);
        
        setTimeout(() => {
            console.log(this.name);  // 'Outer' (inherits from regularFn)
        }, 100);
    }
};

// Explicit binding
function greet() {
    console.log(`Hello, ${this.name}`);
}

const person1 = { name: 'John' };
const person2 = { name: 'Jane' };

greet.call(person1);   // 'Hello, John'
greet.call(person2);   // 'Hello, Jane'
greet.apply(person1);  // Same as call, but args as array
greet.bind(person1);   // Returns new function with 'this' bound
```

### Object Destructuring

**Definition:** Object destructuring is an ES6 syntax that extracts properties from an object into named variables in a single statement. Unlike array destructuring (which is positional), object destructuring matches by property name. You can rename variables, set default values, and use rest syntax (`...rest`) to collect remaining properties into a new object.

```javascript
const person = {
    firstName: 'John',
    lastName: 'Doe',
    age: 30,
    address: {
        city: 'New York',
        country: 'USA'
    }
};

// Basic destructuring
const { firstName, lastName } = person;
console.log(firstName, lastName);  // 'John Doe'

// With different variable names
const { firstName: first, lastName: last } = person;
console.log(first, last);  // 'John Doe'

// Default values
const { middleName = 'N/A' } = person;
console.log(middleName);  // 'N/A'

// Nested destructuring
const { address: { city, country } } = person;
console.log(city, country);  // 'New York USA'

// Rest properties (ES2018)
const { firstName: fn, ...rest } = person;
console.log(fn);    // 'John'
console.log(rest);  // { lastName: 'Doe', age: 30, address: {...} }

// Destructuring in function parameters
function displayUser({ firstName, lastName, age = 0 }) {
    console.log(`${firstName} ${lastName}, ${age}`);
}
displayUser(person);

// Nested array destructuring
const data = {
    results: [
        { id: 1, name: 'Item 1' },
        { id: 2, name: 'Item 2' }
    ]
};
const { results: [firstItem] } = data;
console.log(firstItem);  // { id: 1, name: 'Item 1' }
```

### Object Spread

**Definition:** The object spread operator (`...`) creates a shallow copy of an object's enumerable own properties into a new object. It is commonly used to merge objects, override specific properties, and create immutable updates (spreading into a new object instead of mutating). Later properties override earlier ones when keys conflict.

```javascript
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };

// Combine objects
const combined = { ...obj1, ...obj2 };  // { a: 1, b: 2, c: 3, d: 4 }

// Shallow copy
const copy = { ...obj1 };  // { a: 1, b: 2 }

// Override properties
const modified = { ...obj1, b: 99, e: 5 };  // { a: 1, b: 99, e: 5 }

// Add new properties
const extended = { ...obj1, c: 3, ...obj2 };

// Merge with defaults
const defaults = { theme: 'light', lang: 'en' };
const userSettings = { theme: 'dark' };
const settings = { ...defaults, ...userSettings };  // { theme: 'dark', lang: 'en' }
```

### Object Methods (Static)

```javascript
const person = {
    name: 'John',
    age: 30,
    city: 'New York'
};

// Object.keys() - array of keys
console.log(Object.keys(person));  // ['name', 'age', 'city']

// Object.values() - array of values (ES2017)
console.log(Object.values(person));  // ['John', 30, 'New York']

// Object.entries() - array of [key, value] pairs (ES2017)
console.log(Object.entries(person));
// [['name', 'John'], ['age', 30], ['city', 'New York']]

// Object.fromEntries() - convert entries back to object (ES2019)
const entries = [['a', 1], ['b', 2]];
const obj = Object.fromEntries(entries);  // { a: 1, b: 2 }

// Object.assign() - copy properties (shallow)
const target = { a: 1 };
const source = { b: 2, c: 3 };
Object.assign(target, source);  // target is now { a: 1, b: 2, c: 3 }

// Object.freeze() - make immutable
const frozen = Object.freeze({ a: 1 });
// frozen.a = 2;  // ERROR in strict mode (ignored otherwise)

// Object.seal() - prevent adding/removing properties, but can modify existing
const sealed = Object.seal({ a: 1 });
sealed.a = 2;  // OK
// sealed.b = 3;  // ERROR - can't add new

// Object.getOwnPropertyNames() - all own property names
// Object.getOwnPropertySymbols() - all own symbol properties
// Object.getPrototypeOf() / Object.setPrototypeOf() - prototype manipulation
```

### Getters & Setters

**Definition:** Getters and setters are special methods that define computed properties on objects. A **getter** (`get propName()`) is called when the property is read and can compute a value dynamically. A **setter** (`set propName(value)`) is called when the property is assigned and can validate or transform the value. They look like regular properties to the caller but execute code behind the scenes.

```javascript
const user = {
    firstName: 'John',
    lastName: 'Doe',
    
    // Getter - computed property
    get fullName() {
        return `${this.firstName} ${this.lastName}`;
    },
    
    // Setter
    set fullName(name) {
        [this.firstName, this.lastName] = name.split(' ');
    },
    
    // Getter with private backing
    _age: 30,
    get age() {
        return this._age;
    },
    set age(value) {
        if (value < 0 || value > 150) {
            throw new Error('Invalid age');
        }
        this._age = value;
    }
};

console.log(user.fullName);  // 'John Doe'
user.fullName = 'Jane Smith';
console.log(user.firstName); // 'Jane'

// Define getter/setter with Object.defineProperty
const product = { price: 100 };
Object.defineProperty(product, 'priceWithTax', {
    get() {
        return this.price * 1.2;
    },
    enumerable: true,
    configurable: true
});
```

---

## 8. DOM Manipulation

### Definition
The Document Object Model (DOM) is a programming interface for HTML documents. JavaScript can read and modify the DOM to create dynamic web pages, respond to user interactions, and update content without reloading the page.

The DOM represents the page structure as a tree of objects, allowing JavaScript to access and manipulate HTML elements, their attributes, styles, and content programmatically.

### DOM Tree Structure

**Definition:** The DOM (Document Object Model) is a tree-shaped in-memory representation of an HTML document. Each HTML element becomes a **node** in the tree: the `document` is the root, `<html>` is its child, `<head>` and `<body>` are siblings, and so on. JavaScript uses the DOM API to read, create, modify, and delete nodes, making web pages dynamic and interactive.

```
┌─────────────────────────────────────────────────────────┐
│                  DOM TREE STRUCTURE                     │
├─────────────────────────────────────────────────────────┤
│                                                         │
│                      document                           │
│                         │                               │
│                         ▼                               │
│                      <html>                             │
│                         │                               │
│        ┌────────────────┼────────────────┐              │
│        ▼                ▼                ▼              │
│      <head>          <body>             ...             │
│        │                │                               │
│        ▼                ▼                               │
│     <title>      ┌──────┴──────┐                        │
│   "My Page"      ▼             ▼                        │
│                 <div>       <script>                    │
│               id="app"                                  │
│                  │                                      │
│      ┌───────────┼───────────┐                          │
│      ▼           ▼           ▼                          │
│    <h1>        <p>        <button>                      │
│   "Hello"    "Text"      "Click"                        │
│      │           │           │                          │
│   Text Node  Text Node  Text Node                       │
│                                                         │
│  Relationships:                                         │
│  • parentNode/Element                                   │
│  • childNodes/children                                  │
│  • firstChild/firstElementChild                         │
│  • lastChild/lastElementChild                           │
│  • nextSibling/nextElementSibling                       │
│  • previousSibling/previousElementSibling               │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Selecting Elements

**Definition:** DOM selection methods find HTML elements in the document so JavaScript can interact with them. `getElementById()` selects by ID (fastest, returns one element), `querySelector()` selects the first element matching a CSS selector, `querySelectorAll()` returns all matches as a NodeList, and `getElementsByClassName()`/`getElementsByTagName()` return live HTMLCollections.

```javascript
// getElementById - single element by ID (fastest)
const header = document.getElementById('header');

// querySelector - first match of CSS selector
const firstButton = document.querySelector('.btn');
const navLink = document.querySelector('nav a');
const submitBtn = document.querySelector('button[type="submit"]');

// querySelectorAll - all matches (returns NodeList)
const allButtons = document.querySelectorAll('.btn');
const paragraphs = document.querySelectorAll('p');

// getElementsByClassName - live HTMLCollection
const items = document.getElementsByClassName('item');

// getElementsByTagName - live HTMLCollection
const divs = document.getElementsByTagName('div');

// getElementsByName (for form elements)
const radios = document.getElementsByName('gender');

// Selecting from element (scoped selection)
const nav = document.querySelector('nav');
const navLinks = nav.querySelectorAll('a');  // Only links inside nav

// Converting NodeList to Array
const buttonsArray = Array.from(document.querySelectorAll('.btn'));
// or
const buttonsArray2 = [...document.querySelectorAll('.btn')];
```

### Modifying Content

**Definition:** DOM content can be modified using `textContent` (sets/gets text, safe from XSS), `innerHTML` (sets/gets HTML markup — use carefully as it can introduce XSS vulnerabilities), and `innerText` (like `textContent` but respects CSS visibility). For inserting adjacent HTML without replacing existing content, use `insertAdjacentHTML()`.

```javascript
const element = document.getElementById('example');

// textContent - plain text (safer, faster)
element.textContent = 'Hello World';
console.log(element.textContent);  // Gets all text content

// innerHTML - HTML content (can be security risk with user input)
element.innerHTML = '<strong>Bold</strong> text';
console.log(element.innerHTML);  // Gets HTML as string

// innerText - rendered text (considers CSS, slower)
element.innerText = 'Visible text only';

// outerHTML - element with content
element.outerHTML = '<div id="new">Replaced</div>';

// Inserting HTML (safer alternatives to innerHTML)
const container = document.getElementById('container');

// insertAdjacentHTML - positions: 'beforebegin', 'afterbegin', 'beforeend', 'afterend'
container.insertAdjacentHTML('beforeend', '<p>New paragraph</p>');

// Creating elements (safer than innerHTML)
const newDiv = document.createElement('div');
newDiv.textContent = 'Safe content';
container.appendChild(newDiv);
```

### Modifying Attributes

**Definition:** HTML element attributes are read and modified using `getAttribute(name)`, `setAttribute(name, value)`, `removeAttribute(name)`, and `hasAttribute(name)`. For standard attributes (like `src`, `href`, `id`), direct property access (`element.src`) is faster and more convenient. For custom data attributes (`data-*`), use the `dataset` property.

```javascript
const link = document.querySelector('a');
const input = document.querySelector('input');
const img = document.querySelector('img');

// getAttribute / setAttribute / removeAttribute
link.setAttribute('href', 'https://example.com');
link.setAttribute('target', '_blank');
const href = link.getAttribute('href');
link.removeAttribute('target');

// Direct property access (for standard attributes)
input.type = 'email';
input.name = 'email';
input.placeholder = 'Enter email';
input.value = 'user@example.com';
input.disabled = true;
input.checked = false;

img.src = 'photo.jpg';
img.alt = 'Description';
img.width = 300;

// Data attributes (data-*)
const element = document.querySelector('[data-user-id]');
const userId = element.dataset.userId;  // data-user-id
const userRole = element.dataset.userRole;  // data-user-role

// Set data attributes
element.dataset.status = 'active';  // Creates data-status="active"
```

### Modifying Classes

**Definition:** The `classList` API provides methods to add, remove, toggle, and check CSS classes on elements without overwriting the entire `className` string. Key methods: `classList.add()`, `classList.remove()`, `classList.toggle()` (adds if absent, removes if present), and `classList.contains()` (returns boolean). This is the preferred way to manipulate classes in modern JavaScript.

```javascript
const element = document.getElementById('box');

// className - get/set entire class string
console.log(element.className);  // 'btn primary'
element.className = 'btn secondary';  // Replaces all classes

// classList - modern API (preferred)
element.classList.add('active');
element.classList.remove('disabled');
element.classList.toggle('visible');  // Add if absent, remove if present
element.classList.toggle('hidden', condition);  // Force add/remove based on condition

// Check if has class
if (element.classList.contains('active')) {
    console.log('Element is active');
}

// Replace class
element.classList.replace('old-class', 'new-class');

// Multiple classes at once
element.classList.add('class1', 'class2', 'class3');
```

### Modifying Styles

**Definition:** Inline styles are set via the `element.style` property using camelCase property names (`element.style.backgroundColor = 'red'`). To read computed styles (including those from CSS files), use `window.getComputedStyle(element)`. Prefer toggling CSS classes over setting inline styles directly — it keeps styling in CSS and is easier to maintain.

```javascript
const element = document.getElementById('box');

// Inline styles (element.style)
element.style.color = 'red';
element.style.backgroundColor = 'blue';  // camelCase for CSS properties
element.style.fontSize = '16px';
element.style.marginTop = '10px';
element.style.display = 'none';

// Multiple styles
element.style.cssText = 'color: red; background: blue; padding: 10px;';

// Get computed styles (including from CSS files)
const styles = getComputedStyle(element);
console.log(styles.color);
console.log(styles.getPropertyValue('font-size'));

// CSS custom properties (variables)
element.style.setProperty('--main-color', 'blue');
const mainColor = element.style.getPropertyValue('--main-color');
element.style.removeProperty('--main-color');
```

### Creating, Inserting & Removing Elements

**Definition:** New DOM elements are created with `document.createElement(tag)`, configured with properties and attributes, then inserted into the document using methods like `append()`, `prepend()`, `insertBefore()`, or `insertAdjacentElement()`. Elements are removed with `element.remove()` or `parent.removeChild(element)`. `DocumentFragment` batches multiple insertions for better performance.

```javascript
// Create element
const newDiv = document.createElement('div');
newDiv.className = 'container';
newDiv.id = 'main-container';
newDiv.textContent = 'New Container';

// Add attributes
newDiv.setAttribute('data-id', '123');

// Add styles
newDiv.style.padding = '20px';

// Insert into DOM
const parent = document.getElementById('parent');

// append - add at end (can add multiple nodes/text)
parent.append(newDiv);
parent.append('Text node', anotherElement);

// appendChild - add at end (single node only, returns added node)
const added = parent.appendChild(newDiv);

// prepend - add at beginning
parent.prepend(newDiv);

// insertBefore
const reference = document.getElementById('reference');
parent.insertBefore(newDiv, reference);

// insertAdjacentElement - positions: 'beforebegin', 'afterbegin', 'beforeend', 'afterend'
reference.insertAdjacentElement('afterend', newDiv);

// Replace element
parent.replaceChild(newDiv, oldElement);

// Remove element
newDiv.remove();  // Modern (ES6+)
parent.removeChild(newDiv);  // Older method (returns removed element)

// Clone element
const clone = newDiv.cloneNode();  // Shallow clone (no children)
const deepClone = newDiv.cloneNode(true);  // Deep clone (with children)

// Document fragments (batch insertions for performance)
const fragment = document.createDocumentFragment();
for (let i = 0; i < 100; i++) {
    const item = document.createElement('div');
    item.textContent = `Item ${i}`;
    fragment.appendChild(item);
}
parent.appendChild(fragment);  // Single DOM insertion
```

### Traversing the DOM

**Definition:** DOM traversal means navigating the tree structure to find related elements. Key properties: `parentElement` (parent node), `children` (direct child elements), `firstElementChild`/`lastElementChild`, `nextElementSibling`/`previousElementSibling`. Use `closest(selector)` to find the nearest ancestor matching a CSS selector — essential for event delegation.

```javascript
const element = document.getElementById('current');

// Parent
const parent = element.parentNode;           // Any parent node
const parentElement = element.parentElement; // Parent element only
const closestNav = element.closest('nav');   // Closest ancestor matching selector

// Children
const children = element.childNodes;         // All child nodes (includes text)
const childElements = element.children;      // Only element children
const firstChild = element.firstChild;       // First node
const firstElement = element.firstElementChild;  // First element
const lastChild = element.lastChild;
const lastElement = element.lastElementChild;

// Siblings
const next = element.nextSibling;            // Next node
const nextElement = element.nextElementSibling;  // Next element
const previous = element.previousSibling;
const previousElement = element.previousElementSibling;

// Check relationships
console.log(element.hasChildNodes());
console.log(parent.contains(element));

// Iterate children
Array.from(element.children).forEach(child => {
    console.log(child);
});

// matches() - check if element matches selector
if (element.matches('.active')) {
    console.log('Element has active class');
}
```

---

## 9. Events

### Definition
Events are actions or occurrences that happen in the browser (user interactions, page loading, etc.). JavaScript can listen and respond to these events, enabling interactive web applications.

The event system is the foundation of user interaction in web applications, allowing code to execute in response to clicks, keyboard input, form submissions, page loads, and many other actions.

### Event Propagation Flow

```
┌─────────────────────────────────────────────────────────┐
│              EVENT PROPAGATION PHASES                   │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  User clicks on <button> inside nested structure:       │
│                                                         │
│  ┌────────────────────────────────────────────────┐    │
│  │                    document                     │    │
│  │  1. CAPTURING PHASE (Top to Bottom)            │    │
│  │     ▼                                          │    │
│  │  ┌──────────────────────────────────────────┐  │    │
│  │  │                 <html>                    │  │    │
│  │  │     ▼                                     │  │    │
│  │  │  ┌────────────────────────────────────┐   │  │    │
│  │  │  │              <body>                 │   │  │    │
│  │  │  │     ▼                               │   │  │    │
│  │  │  │  ┌──────────────────────────────┐    │   │  │    │
│  │  │  │  │           <div>               │    │   │  │    │
│  │  │  │  │     ▼                         │    │   │  │    │
│  │  │  │  │  ┌────────────────────────┐   │    │   │  │    │
│  │  │  │  │  │      <button>          │   │    │   │  │    │
│  │  │  │  │  │  2. TARGET PHASE       │   │    │   │  │    │
│  │  │  │  │  └────────────────────────┘   │    │   │  │    │
│  │  │  │  │     ▲                         │    │   │  │    │
│  │  │  │  └───────────────────────────────┘    │   │  │    │
│  │  │  │     ▲                                   │   │  │    │
│  │  │  └─────────────────────────────────────────┘   │  │    │
│  │  │     ▲                                            │  │    │
│  │  └──────────────────────────────────────────────────┘  │    │
│  │     ▲                                                   │    │
│  └─────────────────────────────────────────────────────────┘    │
│                                                         │
│  3. BUBBLING PHASE (Bottom to Top) - default            │
│                                                         │
│  Use event.stopPropagation() to stop propagation       │
│  Use {capture: true} to handle event in capture phase   │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### addEventListener

```javascript
const button = document.getElementById('myButton');

// Basic event listener
button.addEventListener('click', function(event) {
    console.log('Button clicked!');
});

// With arrow function
button.addEventListener('click', (event) => {
    console.log('Clicked!', event.target);
});

// Named function (can remove later)
function handleClick(event) {
    console.log('Clicked!');
}
button.addEventListener('click', handleClick);

// Remove event listener
button.removeEventListener('click', handleClick);

// Multiple listeners (executed in order)
button.addEventListener('click', () => console.log('First'));
button.addEventListener('click', () => console.log('Second'));

// Options (ES6)
button.addEventListener('click', handler, {
    once: true,        // Auto-remove after first trigger
    capture: false,    // Use bubbling (default) or capturing
    passive: true      // Won't call preventDefault (better for scroll/touch)
});

// Older onevent properties (limited - only one handler)
button.onclick = function() {
    console.log('Clicked');
};
button.onclick = null;  // Remove
```

### Common Events

**Definition:** Browser events are actions or occurrences that happen in the browser that JavaScript can respond to. Common categories: **Mouse events** (`click`, `dblclick`, `mouseover`, `mouseout`, `mousemove`), **Keyboard events** (`keydown`, `keyup`, `keypress`), **Form events** (`submit`, `change`, `input`, `focus`, `blur`), and **Window events** (`load`, `DOMContentLoaded`, `resize`, `scroll`).

```javascript
// Mouse events
const element = document.getElementById('box');

element.addEventListener('click', () => console.log('Single click'));
element.addEventListener('dblclick', () => console.log('Double click'))
element.addEventListener('mousedown', () => console.log('Mouse down'));
element.addEventListener('mouseup', () => console.log('Mouse up'));
element.addEventListener('mouseenter', () => console.log('Entered'));
element.addEventListener('mouseleave', () => console.log('Left'));
element.addEventListener('mousemove', () => console.log('Moving'));
element.addEventListener('contextmenu', (e) => {
    e.preventDefault();  // Disable right-click menu
    console.log('Right clicked');
});

// Keyboard events
document.addEventListener('keydown', (e) => {
    console.log('Key pressed:', e.key);       // 'a', 'Enter', 'ArrowUp'
    console.log('Key code:', e.code);         // 'KeyA', 'Enter'
    console.log('Ctrl pressed:', e.ctrlKey);
    console.log('Shift pressed:', e.shiftKey);
    
    if (e.key === 'Enter' && e.ctrlKey) {
        console.log('Ctrl+Enter pressed');
    }
});

document.addEventListener('keyup', (e) => {
    console.log('Key released:', e.key);
});

// Form events
const form = document.querySelector('form');
const input = document.querySelector('input');

input.addEventListener('focus', () => console.log('Input focused'));
input.addEventListener('blur', () => console.log('Input blurred'));
input.addEventListener('input', (e) => {
    console.log('Value changed:', e.target.value);
});
input.addEventListener('change', (e) => {
    console.log('Value committed:', e.target.value);  // On blur for text
});

form.addEventListener('submit', (e) => {
    e.preventDefault();  // Prevent page reload
    const formData = new FormData(form);
    console.log('Submitted:', Object.fromEntries(formData));
});

// Window/Document events
window.addEventListener('load', () => {
    console.log('Page fully loaded');
});

document.addEventListener('DOMContentLoaded', () => {
    console.log('DOM ready (before images load)');
});

window.addEventListener('resize', () => {
    console.log('Window resized:', window.innerWidth);
});

window.addEventListener('scroll', () => {
    console.log('Scrolled:', window.scrollY);
});

// Touch events (mobile)
element.addEventListener('touchstart', (e) => {
    console.log('Touch started');
});
element.addEventListener('touchmove', (e) => {
    console.log('Touch moving');
});
element.addEventListener('touchend', (e) => {
    console.log('Touch ended');
});
```

### The Event Object

**Definition:** When an event fires, the browser creates an **Event object** and passes it to the event handler. It contains information about the event: `event.type` (event name), `event.target` (element that triggered the event), `event.currentTarget` (element the listener is attached to), `event.key` (for keyboard events), `event.clientX`/`event.clientY` (for mouse events), and methods like `preventDefault()` and `stopPropagation()`.

```javascript
document.addEventListener('click', (event) => {
    // Target elements
    console.log(event.target);        // Element that triggered event
    console.log(event.currentTarget); // Element listener is attached to
    
    // Mouse position
    console.log(event.clientX, event.clientY);  // Relative to viewport
    console.log(event.pageX, event.pageY);      // Relative to document
    console.log(event.offsetX, event.offsetY);  // Relative to target
    
    // Event type
    console.log(event.type);  // 'click'
    
    // Time
    console.log(event.timeStamp);  // Milliseconds since page load
    
    // Prevent default action
    event.preventDefault();
    
    // Stop propagation
    event.stopPropagation();
    
    // Immediate stop (stops other listeners on same element)
    event.stopImmediatePropagation();
});
```

### Event Delegation

**Definition:** Event delegation is a pattern where a single event listener is attached to a parent element to handle events from its children, using the fact that events bubble up the DOM. Instead of adding listeners to each child (expensive and doesn't work for dynamically added elements), you listen on the parent and check `event.target` to identify which child triggered the event.

```javascript
// Instead of adding listeners to each item (inefficient for many items)
// Add single listener to parent, use event.target

const list = document.getElementById('todo-list');

// Bad: Adding listener to each item
// document.querySelectorAll('li').forEach(li => {
//     li.addEventListener('click', handleClick);
// });

// Good: Event delegation
list.addEventListener('click', (e) => {
    // Check if clicked element is a list item
    if (e.target.matches('li')) {
        console.log('Clicked item:', e.target.textContent);
        e.target.classList.toggle('completed');
    }
    
    // Or use closest for nested elements
    const button = e.target.closest('.delete-btn');
    if (button) {
        const item = button.closest('li');
        item.remove();
    }
});

// Add new items dynamically - no new listeners needed!
const newItem = document.createElement('li');
newItem.textContent = 'New Item';
list.appendChild(newItem);  // Automatically works with delegation
```

### Event Propagation

**Definition:** Event propagation describes the order in which event handlers are called when an event occurs on a nested element. It has three phases: **capturing** (event travels from window down to the target), **target** (event reaches the element), and **bubbling** (event travels back up to the window). By default, handlers use the bubbling phase. `stopPropagation()` prevents the event from continuing up or down the chain.

```javascript
// Event propagation: Capturing (down) → Target → Bubbling (up)

// Bubbling phase (default) - inner to outer
document.getElementById('inner').addEventListener('click', () => {
    console.log('Inner clicked');  // 1st
});
document.getElementById('outer').addEventListener('click', () => {
    console.log('Outer clicked');  // 2nd
});
document.body.addEventListener('click', () => {
    console.log('Body clicked');   // 3rd
});

// Capturing phase (rarely used) - outer to inner
document.getElementById('outer').addEventListener('click', () => {
    console.log('Outer (capturing)');  // 1st
}, true);  // Use capture phase

// Stop propagation
button.addEventListener('click', (e) => {
    e.stopPropagation();  // Stop bubbling up
    console.log('Button clicked');
});
```

### preventDefault

**Definition:** `event.preventDefault()` cancels the browser's default action for an event without stopping propagation. Common uses: preventing form submission to handle it with JavaScript, preventing link navigation, preventing right-click context menus. It does not stop the event from bubbling — use `stopPropagation()` for that.

```javascript
// Prevent default browser behavior

// Prevent form submission
form.addEventListener('submit', (e) => {
    e.preventDefault();
    // Handle form with JavaScript (AJAX, validation, etc.)
});

// Prevent link navigation
link.addEventListener('click', (e) => {
    e.preventDefault();
    // Handle navigation with JavaScript (SPA routing)
});

// Prevent context menu
document.addEventListener('contextmenu', (e) => {
    e.preventDefault();
    // Show custom context menu
});

// Check if default was prevented
if (event.defaultPrevented) {
    console.log('Default was prevented');
}
```

---

## 10. Asynchronous JavaScript

### Definition
Asynchronous programming allows code to run without blocking the main thread, essential for operations like network requests, timers, and file I/O that would otherwise freeze the user interface.

JavaScript uses an event-driven, non-blocking I/O model that enables handling multiple operations concurrently through callbacks, promises, and async/await syntax.

### Event Loop Architecture

```
┌─────────────────────────────────────────────────────────┐
│                 EVENT LOOP MECHANISM                    │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌─────────────────┐                                    │
│  │   CALL STACK    │                                    │
│  │                 │                                    │
│  │  main()         │                                    │
│  │    │            │                                    │
│  │    ▼            │                                    │
│  │  setTimeout()   │──────────┐                         │
│  │  fetch()        │──┐       │                         │
│  │  console.log    │  │       │                         │
│  │                 │  │       │                         │
│  └─────────────────┘  │       │                         │
│           │           │       │                         │
│           ▼           ▼       ▼                         │
│  ┌──────────────────────────────────────────────┐      │
│  │            WEB APIs / NODE APIs              │      │
│  │  (Browser: setTimeout, fetch, DOM)           │      │
│  │  (Node: fs, http, timers)                    │      │
│  └──────────────┬───────────────┬───────────────┘      │
│                 │               │                       │
│                 ▼               ▼                       │
│  ┌─────────────────────────┐ ┌─────────────────────┐   │
│  │    CALLBACK QUEUE       │ │  MICROTASK QUEUE    │   │
│  │  (setTimeout, I/O)      │ │  (Promises, queue)  │   │
│  │                         │ │                     │   │
│  │  [callback1]            │ │  [microtask1]       │   │
│  │  [callback2]            │ │  [microtask2]       │   │
│  └───────────┬─────────────┘ └──────────┬──────────┘   │
│              │                          │              │
│              └──────────┬───────────────┘              │
│                         │                               │
│                         ▼                               │
│  ┌────────────────────────────────────────────────┐    │
│  │              EVENT LOOP                        │    │
│  │                                                │    │
│  │  1. Check if Call Stack is empty               │    │
│  │  2. Execute all Microtasks (Promises first)    │    │
│  │  3. Execute one Callback                       │    │
│  │  4. Repeat                                     │    │
│  │                                                │    │
│  │  PRIORITY: Microtasks > Callbacks              │    │
│  └────────────────────────────────────────────────┘    │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Promise States and Flow

```
┌─────────────────────────────────────────────────────────┐
│                 PROMISE LIFECYCLE                       │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌────────────────────────────────────────────────┐    │
│  │          new Promise(executor)                 │    │
│  └──────────────────┬─────────────────────────────┘    │
│                     │                                   │
│                     ▼                                   │
│  ┌────────────────────────────────────────────────┐    │
│  │              PENDING State                     │    │
│  │         (asynchronous operation running)       │    │
│  └──────────────────┬─────────────────────────────┘    │
│                     │                                   │
│         ┌───────────┴───────────┐                       │
│         ▼                       ▼                       │
│  ┌──────────────┐       ┌──────────────┐               │
│  │   resolve()  │       │   reject()   │               │
│  │   (success)  │       │   (failure)  │               │
│  └──────┬───────┘       └──────┬───────┘               │
│         │                      │                        │
│         ▼                      ▼                        │
│  ┌──────────────┐       ┌──────────────┐               │
│  │  FULFILLED   │       │   REJECTED   │               │
│  │              │       │              │               │
│  │  .then()     │       │  .catch()    │               │
│  │  .finally()  │       │  .finally()  │               │
│  └──────────────┘       └──────────────┘               │
│                                                         │
│  Chain: .then().then().catch().finally()                │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Async/Await Execution Flow

```
┌─────────────────────────────────────────────────────────┐
│              ASYNC/AWAIT EXECUTION                      │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  async function fetchData() {                          │
│                                                         │
│      ┌─────────────────────────────────────┐           │
│      │  const user = await fetchUser();    │           │
│      │           │                         │           │
│      │           ▼                         │           │
│      │  [PAUSE - wait for Promise]         │           │
│      │           │                         │           │
│      │           ▼                         │           │
│      │  const orders = await fetchOrders();│           │
│      │           │                         │           │
│      │           ▼                         │           │
│      │  [PAUSE - wait for Promise]         │           │
│      │           │                         │           │
│      │           ▼                         │           │
│      │  return { user, orders };           │           │
│      └─────────────────────────────────────┘           │
│  }                                                     │
│                                                         │
│  Execution:                                            │
│  1. Start fetchData()                                  │
│  2. Pause at await (return Promise to caller)          │
│  3. When resolved, resume where left off               │
│  4. Next await - pause again                           │
│  5. Return final value                                 │
│                                                         │
│  Looks synchronous, works asynchronously               │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### setTimeout & setInterval

**Definition:** `setTimeout(fn, delay)` schedules a function to run once after a specified delay (in milliseconds). `setInterval(fn, interval)` schedules a function to run repeatedly at a fixed interval. Both return an ID that can be passed to `clearTimeout()` or `clearInterval()` to cancel them. They are part of the Web API — not JavaScript itself — and run after the current call stack is empty.

```javascript
// setTimeout - execute once after delay (in milliseconds)
const timeoutId = setTimeout(() => {
    console.log('Executed after 2 seconds');
}, 2000);

// Cancel timeout
clearTimeout(timeoutId);

// Pass arguments
setTimeout((name, age) => {
    console.log(`Hello ${name}, you are ${age}`);
}, 1000, 'John', 30);

// setInterval - execute repeatedly
const intervalId = setInterval(() => {
    console.log('Every 3 seconds');
}, 3000);

// Cancel interval
clearInterval(intervalId);

// Self-correcting interval (accounts for execution time)
function accurateInterval(callback, delay) {
    let expected = Date.now() + delay;
    
    function step() {
        const drift = Date.now() - expected;
        callback();
        expected += delay;
        setTimeout(step, Math.max(0, delay - drift));
    }
    
    setTimeout(step, delay);
}

// setImmediate (Node.js) / requestAnimationFrame (browser)
requestAnimationFrame(() => {
    console.log('Before next paint');
});
```

### Callbacks

**Definition:** In asynchronous JavaScript, a callback is a function passed to an async operation (like `setTimeout`, `fetch`, or file reading) to be called when the operation completes. While callbacks work, deeply nested callbacks create "callback hell" — hard-to-read, hard-to-maintain pyramid-shaped code. Promises and async/await were introduced to solve this problem.

```javascript
// Traditional callback pattern
function fetchUser(userId, callback) {
    setTimeout(() => {
        const user = { id: userId, name: 'John' };
        callback(null, user);  // Error-first callback convention
    }, 1000);
}

fetchUser(1, (error, user) => {
    if (error) {
        console.error('Error:', error);
        return;
    }
    console.log('User:', user);
});

// Callback hell (avoid with Promises/async-await)
fetchUser(1, (err, user) => {
    if (err) return;
    fetchOrders(user.id, (err, orders) => {
        if (err) return;
        fetchProducts(orders[0].id, (err, products) => {
            if (err) return;
            console.log(products);
        });
    });
});
```

### Promises

**Definition:** A Promise is an object representing the eventual completion or failure of an asynchronous operation. It has three states: **pending** (initial), **fulfilled** (operation succeeded, `.then()` is called), and **rejected** (operation failed, `.catch()` is called). Promises can be chained with `.then()` for sequential async operations and combined with `Promise.all()` for parallel operations.

```javascript
// Creating a Promise
const promise = new Promise((resolve, reject) => {
    // Async operation
    setTimeout(() => {
        const success = true;
        if (success) {
            resolve('Operation completed');
        } else {
            reject(new Error('Operation failed'));
        }
    }, 1000);
});

// Consuming a Promise
promise
    .then(result => {
        console.log('Success:', result);
        return result + '!';
    })
    .then(modified => {
        console.log('Modified:', modified);
    })
    .catch(error => {
        console.error('Error:', error.message);
    })
    .finally(() => {
        console.log('Cleanup (always runs)');
    });

// Chaining Promises
function fetchUser(id) {
    return new Promise((resolve) => {
        setTimeout(() => resolve({ id, name: 'John' }), 500);
    });
}

function fetchOrders(userId) {
    return new Promise((resolve) => {
        setTimeout(() => resolve([{ id: 1, total: 100 }]), 500);
    });
}

fetchUser(1)
    .then(user => {
        console.log('User:', user);
        return fetchOrders(user.id);  // Return new Promise
    })
    .then(orders => {
        console.log('Orders:', orders);
    })
    .catch(error => {
        console.error('Any error in chain:', error);
    });

// Promise static methods
Promise.resolve('immediate value');
Promise.reject(new Error('immediate error'));

// Create resolved/rejected promises
const resolved = Promise.resolve(42);
const rejected = Promise.reject(new Error('Fail'));
```

### Async/Await (ES2017)

**Definition:** `async/await` is syntactic sugar over Promises that makes asynchronous code look and behave like synchronous code. An `async` function always returns a Promise. The `await` keyword pauses execution inside the async function until the Promise resolves, then returns the resolved value. Use `try/catch` for error handling. `await` can only be used inside `async` functions.

```javascript
// async function always returns a Promise
async function fetchData() {
    return 'data';  // Implicitly wrapped in Promise.resolve()
}

// await pauses execution until Promise resolves
async function getUserData() {
    try {
        const user = await fetchUser(1);
        console.log('User:', user);
        
        const orders = await fetchOrders(user.id);
        console.log('Orders:', orders);
        
        return { user, orders };
    } catch (error) {
        console.error('Error:', error);
        throw error;  // Re-throw or handle
    }
}

// Sequential vs Parallel execution
async function sequential() {
    // Runs one after another (slower)
    const user = await fetchUser(1);
    const orders = await fetchOrders(1);
    const products = await fetchProducts();
    return { user, orders, products };
}

async function parallel() {
    // Runs simultaneously (faster)
    const [user, orders, products] = await Promise.all([
        fetchUser(1),
        fetchOrders(1),
        fetchProducts()
    ]);
    return { user, orders, products };
}

async function parallelFetch(userId) {
    // Start both at same time
    const userPromise = fetchUser(userId);
    const ordersPromise = fetchOrders(userId);
    
    // Wait for both
    const user = await userPromise;
    const orders = await ordersPromise;
    
    return { user, orders };
}

// Top-level await (ES2022, modules only)
// const data = await fetch('/api/data');
```

### Fetch API

**Definition:** The Fetch API is a modern, Promise-based interface for making HTTP requests from the browser. It replaces the older `XMLHttpRequest`. `fetch(url)` returns a Promise that resolves to a `Response` object. The response body must be parsed separately (`.json()`, `.text()`, `.blob()`). By default, fetch only rejects on network errors — HTTP error status codes (4xx, 5xx) must be checked manually.

```javascript
// Basic GET request
fetch('https://api.example.com/users')
    .then(response => {
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        return response.json();  // Parse JSON
    })
    .then(data => console.log(data))
    .catch(error => console.error('Fetch error:', error));

// With async/await
async function getUsers() {
    try {
        const response = await fetch('https://api.example.com/users');
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        const users = await response.json();
        return users;
    } catch (error) {
        console.error('Error:', error);
        throw error;
    }
}

// POST request
async function createUser(userData) {
    const response = await fetch('https://api.example.com/users', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer token123'
        },
        body: JSON.stringify(userData)
    });
    
    if (!response.ok) {
        throw new Error('Failed to create user');
    }
    
    return response.json();
}

// Other HTTP methods
// PUT - update entire resource
// PATCH - partial update
// DELETE - delete resource

// Request options
fetch(url, {
    method: 'GET',
    headers: {
        'Accept': 'application/json',
        'X-Custom-Header': 'value'
    },
    mode: 'cors',        // cors, no-cors, same-origin
    cache: 'default',    // default, no-store, reload, etc.
    credentials: 'same-origin',  // omit, same-origin, include
    redirect: 'follow',  // follow, error, manual
    referrerPolicy: 'no-referrer'
});

// Abort fetch
const controller = new AbortController();
const signal = controller.signal;

fetch(url, { signal })
    .then(response => response.json())
    .catch(error => {
        if (error.name === 'AbortError') {
            console.log('Fetch aborted');
        }
    });

// Cancel after 5 seconds
setTimeout(() => controller.abort(), 5000);
```

### Promise.all / Promise.race / Promise.allSettled

**Definition:** These static Promise methods handle multiple Promises simultaneously: `Promise.all()` runs all in parallel and resolves when all succeed (rejects immediately if any fail), `Promise.race()` resolves/rejects with the first Promise to settle, `Promise.allSettled()` waits for all to settle regardless of success/failure (returns an array of result objects), and `Promise.any()` resolves with the first fulfilled Promise.

```javascript
// Promise.all - wait for all, fail fast
const promises = [
    fetch('/api/users'),
    fetch('/api/posts'),
    fetch('/api/comments')
];

try {
    const [users, posts, comments] = await Promise.all(promises);
    console.log('All loaded');
} catch (error) {
    console.error('One failed:', error);  // First rejection
}

// Promise.allSettled - wait for all, never rejects (ES2020)
const results = await Promise.allSettled([
    Promise.resolve('success'),
    Promise.reject('error'),
    Promise.resolve('another success')
]);

results.forEach(result => {
    if (result.status === 'fulfilled') {
        console.log('Success:', result.value);
    } else {
        console.log('Failed:', result.reason);
    }
});
// [
//   { status: 'fulfilled', value: 'success' },
//   { status: 'rejected', reason: 'error' },
//   { status: 'fulfilled', value: 'another success' }
// ]

// Promise.race - first to settle wins
const fastest = await Promise.race([
    fetch('/api/endpoint1'),
    fetch('/api/endpoint2'),
    new Promise((_, reject) => 
        setTimeout(() => reject(new Error('Timeout')), 5000)
    )
]);

// Promise.any - first to fulfill (ES2021)
const firstSuccess = await Promise.any([
    fetch('/api/mirror1'),
    fetch('/api/mirror2'),
    fetch('/api/mirror3')
]);
// Returns first successful response, ignores rejections unless all fail
```

---

## 11. ES6+ Features

### Definition
ES6 (ECMAScript 2015) and subsequent versions introduced major improvements to JavaScript, modernizing the language with new syntax, features, and APIs that make code more concise, readable, and powerful.

These features have become the standard for modern JavaScript development, offering better ways to work with variables, functions, objects, modules, and asynchronous code.

### Let & Const

**Definition:** `let` and `const` are block-scoped variable declarations introduced in ES6 to replace `var`. `let` allows reassignment but not redeclaration in the same scope. `const` requires initialization and prevents reassignment of the binding (though objects/arrays declared with `const` can still be mutated). Both are in the Temporal Dead Zone before their declaration line.

```javascript
// Block-scoped variables (vs function-scoped var)
{
    let x = 10;
    const y = 20;
    // x and y only exist in this block
}
// console.log(x);  // ReferenceError

// Temporal dead zone
// console.log(a);  // ReferenceError
let a = 5;

// Const requires initialization
// const b;  // SyntaxError
const b = 10;
// b = 20;   // TypeError - can't reassign

// Const objects can be modified
const obj = { name: 'John' };
obj.name = 'Jane';  // OK
// obj = {};        // TypeError - can't reassign reference

// Best practice: use const by default, let when reassignment needed
```

### Template Literals

```javascript
// Backtick strings with embedded expressions
const name = 'John';
const age = 30;

const message = `Hello, ${name}! You are ${age} years old.`;

// Multi-line strings
const html = `
    <div>
        <h1>${name}</h1>
        <p>Age: ${age}</p>
    </div>
`;

// Expression evaluation
const sum = `2 + 3 = ${2 + 3}`;

// Tagged templates
function highlight(strings, ...values) {
    return strings.reduce((result, string, i) => {
        const value = values[i] ? `<b>${values[i]}</b>` : '';
        return result + string + value;
    }, '');
}

const result = highlight`Hello ${name}, you are ${age}`;
// 'Hello <b>John</b>, you are <b>30</b>'

// Raw strings
const path = String.raw`C:\Users\John\Documents`;
// C:\Users\John\Documents (not interpreted as escape sequences)
```

### Destructuring

**Definition:** Destructuring (ES6) is a syntax that unpacks values from arrays or properties from objects into distinct variables in a single statement. Array destructuring uses position; object destructuring uses property names. Both support default values, renaming, nested destructuring, and rest patterns. Destructuring is widely used in function parameters, React hooks, and API response handling.

```javascript
// Array destructuring
const [a, b] = [1, 2];
const [first, , third] = [1, 2, 3];  // Skip second
const [head, ...tail] = [1, 2, 3, 4];

// Default values
const [x = 0, y = 0] = [1];  // x=1, y=0

// Object destructuring
const { name, age } = { name: 'John', age: 30 };
const { name: firstName, age: years } = person;  // Rename
const { country = 'USA' } = person;  // Default

// Nested destructuring
const { address: { city } } = { address: { city: 'NYC' } };

// Function parameters
function display({ name, age = 0 }) {
    console.log(name, age);
}

// Rest in destructuring
const { a, b, ...rest } = { a: 1, b: 2, c: 3, d: 4 };
```

### Spread & Rest Operators

**Definition:** In ES6+, the spread operator (`...`) expands iterables into individual elements in array literals, function calls, and object literals. The rest operator (`...`) collects remaining elements into an array in function parameters and destructuring. Both use identical syntax but serve opposite purposes: spread expands, rest collects.

```javascript
// Spread in arrays
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];  // [1, 2, 3, 4, 5]
const copy = [...arr1];  // Shallow copy
const merged = [...arr1, ...arr2];

// Spread in objects (ES2018)
const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 };  // { a: 1, b: 2, c: 3 }
const objCopy = { ...obj1 };
const combined = { ...obj1, ...obj2 };

// Rest in function parameters
function sum(...numbers) {
    return numbers.reduce((a, b) => a + b, 0);
}
sum(1, 2, 3, 4);  // 10

// Rest in destructuring
const [first, ...rest] = [1, 2, 3, 4];
const { name, ...otherProps } = person;
```

### Arrow Functions

**Definition:** Arrow functions (ES6) provide a shorter syntax for function expressions and lexically bind `this`. They are ideal for callbacks and functional programming methods (`map`, `filter`, `reduce`). Key differences from regular functions: no `this` binding, no `arguments` object, cannot be used as constructors, and cannot be used as generator functions.

```javascript
// Short syntax
const add = (a, b) => a + b;
const square = x => x * x;
const getRandom = () => Math.random();

// With block (explicit return)
const calculate = (a, b) => {
    const sum = a + b;
    return sum * 2;
};

// Returning object (wrap in parentheses)
const makePerson = (name, age) => ({ name, age });

// No binding of 'this'
const obj = {
    value: 42,
    // Regular function - 'this' is obj
    regularMethod: function() {
        setTimeout(function() {
            console.log(this.value);  // undefined (this is window)
        }, 100);
    },
    // Arrow function - 'this' is obj
    arrowMethod: function() {
        setTimeout(() => {
            console.log(this.value);  // 42 (inherits from arrowMethod)
        }, 100);
    }
};

// Cannot be constructors
// const Person = (name) => { this.name = name; };
// new Person('John');  // TypeError

// No arguments object
const fn = () => {
    // console.log(arguments);  // ReferenceError
};
```

### Modules (Import/Export)

**Definition:** ES6 modules allow splitting JavaScript code into separate files with explicit imports and exports. `export` makes values available to other modules; `import` brings them in. **Named exports** allow multiple exports per file; **default exports** allow one primary export. Modules are always in strict mode, have their own scope, and are loaded asynchronously by the browser.

```javascript
// math.js - Exporting
// Named exports
export const PI = 3.14159;
export function add(a, b) {
    return a + b;
}
export class Calculator {
    multiply(a, b) {
        return a * b;
    }
}

// Default export (one per module)
export default function greet(name) {
    return `Hello, ${name}!`;
}

// Export existing variables
const utils = { helper: () => {} };
export { utils };

// Rename exports
export { add as sum, PI as constantPI };

// Re-export
export { foo, bar } from './other-module.js';
export * from './another-module.js';
export { default as MyComponent } from './Component.js';

// main.js - Importing
// Default import
import greet from './math.js';

// Named imports
import { PI, add, Calculator } from './math.js';

// Import with alias
import { add as sum, PI as constantPI } from './math.js';

// Import all as namespace
import * as math from './math.js';
console.log(math.PI);
console.log(math.add(2, 3));

// Import default and named
import greet, { PI, add } from './math.js';

// Side effects only
import './styles.css';

// Dynamic import (lazy loading)
const module = await import('./heavy-module.js');
module.heavyFunction();

// Conditional import
if (condition) {
    const { feature } = await import('./feature.js');
}
```

### Classes

**Definition:** ES6 classes are syntactic sugar over JavaScript's prototype-based inheritance. They provide a cleaner syntax for creating constructor functions and setting up prototype chains. Classes support `constructor()`, instance methods, static methods, getters/setters, and inheritance via `extends` and `super`. Unlike function declarations, class declarations are NOT hoisted.

```javascript
// Class declaration
class Person {
    // Static property/method - belongs to class, not instance
    static species = 'Homo sapiens';
    static count = 0;
    
    static isHuman(person) {
        return person instanceof Person;
    }
    
    // Constructor
    constructor(name, age) {
        this.name = name;
        this.age = age;
        Person.count++;
    }
    
    // Instance method
    greet() {
        return `Hello, I'm ${this.name}`;
    }
    
    // Getter
    get info() {
        return `${this.name} (${this.age})`;
    }
    
    // Setter
    set birthYear(year) {
        this.age = new Date().getFullYear() - year;
    }
    
    // Private field (ES2022)
    #secret = 'private data';
    
    getSecret() {
        return this.#secret;
    }
    
    // Private method
    #privateMethod() {
        return 'private';
    }
}

// Inheritance
class Employee extends Person {
    constructor(name, age, position) {
        super(name, age);  // Call parent constructor
        this.position = position;
    }
    
    // Override method
    greet() {
        return `${super.greet()} and I work as ${this.position}`;
    }
    
    // Static with inheritance
    static createDeveloper(name, age) {
        return new Employee(name, age, 'Developer');
    }
}

// Usage
const john = new Person('John', 30);
console.log(john.greet());
console.log(Person.species);

const jane = new Employee('Jane', 25, 'Designer');
console.log(jane.greet());
```

### Default Parameters

**Definition:** Default parameters (ES6) allow function parameters to have a fallback value when no argument is passed or when `undefined` is explicitly passed. They are evaluated at call time (not definition time), so each call gets a fresh default. Default parameters can reference earlier parameters and can be any expression, including function calls.

```javascript
function greet(name = 'Guest', greeting = 'Hello') {
    return `${greeting}, ${name}!`;
}

greet();                  // 'Hello, Guest!'
greet('John');            // 'Hello, John!'
greet('John', 'Hi');      // 'Hi, John!'

// Default can be expression
function getTimestamp(date = new Date()) {
    return date.getTime();
}

// Use previous parameters
function createUser(name, email = `${name}@example.com`) {
    return { name, email };
}

// Required parameter check
function required(param) {
    throw new Error(`${param} is required`);
}

function createPost(title = required('title'), content = '') {
    return { title, content };
}
```

### Other ES6+ Features

**Definition:** Beyond the major ES6 features, modern JavaScript includes: template literals (backtick strings with `${expression}` interpolation and multiline support), enhanced object literals (shorthand properties, computed keys, method shorthand), `Symbol` (unique primitive for private-like keys), iterators and generators (`function*`, `yield`), `WeakMap`/`WeakSet` (garbage-collection-friendly collections), and `Proxy`/`Reflect` for metaprogramming.

```javascript
// Enhanced object literals
const name = 'John';
const age = 30;

const person = {
    name,           // Shorthand property
    age,
    greet() {       // Shorthand method
        return `Hi, I'm ${this.name}`;
    },
    ['computed' + 'Key']: 'value',  // Computed property
    [Symbol.iterator]: function*() {  // Symbol as key
        yield this.name;
        yield this.age;
    }
};

// for...of loop
for (const char of 'Hello') {
    console.log(char);
}

// Symbol type
const id = Symbol('id');
const user = {
    [id]: 123,
    name: 'John'
};

// Map and Set
const map = new Map();
map.set('key', 'value');
map.get('key');

const set = new Set([1, 2, 2, 3]);
console.log([...set]);  // [1, 2, 3]

// Generators
function* idGenerator() {
    let id = 1;
    while (true) {
        yield id++;
    }
}
const gen = idGenerator();
console.log(gen.next().value);  // 1
console.log(gen.next().value);  // 2

// Proxies
const handler = {
    get(target, prop) {
        return prop in target ? target[prop] : 'Property not found';
    }
};
const proxy = new Proxy({}, handler);

// Optional chaining (ES2020)
const city = user?.address?.city;
const result = obj?.method?.();

// Nullish coalescing (ES2020)
const value = input ?? 'default';

// BigInt (ES2020)
const huge = 9007199254740991n;

// Logical assignment (ES2021)
obj.prop ??= 'default';  // Assign if null/undefined
obj.prop &&= newValue;   // Assign if truthy
obj.prop ||= fallback;   // Assign if falsy

// at() method (ES2022)
arr.at(-1);  // Last element
arr.at(-2);  // Second to last

// Class fields and private methods (ES2022)
class MyClass {
    publicField = 'public';
    #privateField = 'private';
    
    #privateMethod() {
        return this.#privateField;
    }
}

// Top-level await (ES2022)
// const data = await fetch('/api/data');

// Object.hasOwn() (ES2022)
Object.hasOwn(obj, 'prop');  // Replace obj.hasOwnProperty()

// Array grouping (ES2024 proposal, may need polyfill)
// Object.groupBy(array, item => item.category);
```

---

## 12. Best Practices

### Definition
Best practices in JavaScript are guidelines that help write clean, maintainable, and efficient code. Following these patterns ensures code quality, reduces bugs, and makes collaboration easier.

These practices have evolved through years of community experience and help avoid common pitfalls in JavaScript development.

### DO's ✅

```javascript
// 1. Use strict mode
'use strict';

// 2. Use const by default, let when reassignment needed
const PI = 3.14159;
const config = { apiUrl: '...' };
let count = 0;  // Will be reassigned
let currentUser = null;  // Will be reassigned

// 3. Use meaningful variable names
const userCount = 42;
const isActive = true;
const userList = ['John', 'Jane'];
// Avoid: x, y, data, temp, foo

// 4. Use strict equality (===)
if (value === null) { }  // Good
// if (value == null) { }  // Avoid (also matches undefined)

// 5. Handle errors properly
try {
    const data = JSON.parse(jsonString);
} catch (error) {
    console.error('Invalid JSON:', error.message);
    // Handle gracefully
}

// 6. Use template literals for strings
const message = `Hello, ${name}! You have ${count} messages.`;

// 7. Use destructuring
const { name, email } = user;
const [first, second] = items;

// 8. Use arrow functions for callbacks
const doubled = numbers.map(n => n * 2);

// 9. Use async/await over callbacks
async function fetchData() {
    const response = await fetch('/api/data');
    return response.json();
}

// 10. Document with JSDoc
/**
 * Calculate area of rectangle
 * @param {number} width - The width
 * @param {number} height - The height
 * @returns {number} The calculated area
 */
function calculateArea(width, height) {
    return width * height;
}

// 11. Avoid modifying parameters
function processData(data) {
    const processed = { ...data };  // Copy instead of mutate
    processed.timestamp = Date.now();
    return processed;
}

// 12. Use early returns to reduce nesting
function checkUser(user) {
    if (!user) return null;
    if (!user.isActive) return null;
    if (!user.hasPermission) return null;
    return user.data;
}

// 13. Use array methods over loops
// Good
const adults = users.filter(u => u.age >= 18);
const names = users.map(u => u.name);
const total = prices.reduce((sum, price) => sum + price, 0);

// Avoid
const adults = [];
for (let i = 0; i < users.length; i++) {
    if (users[i].age >= 18) {
        adults.push(users[i]);
    }
}

// 14. Validate inputs
function divide(a, b) {
    if (typeof a !== 'number' || typeof b !== 'number') {
        throw new TypeError('Arguments must be numbers');
    }
    if (b === 0) {
        throw new Error('Cannot divide by zero');
    }
    return a / b;
}

// 15. Use modules to organize code
// utils.js
export const formatDate = (date) => { ... };
export const validateEmail = (email) => { ... };

// app.js
import { formatDate, validateEmail } from './utils.js';
```

### DON'Ts ❌

```javascript
// 1. Don't use var
var name = 'John';  // Use const or let

// 2. Don't modify built-in prototypes
Array.prototype.myMethod = function() { };  // Bad!

// 3. Don't use eval()
eval('console.log("bad")');  // Security risk

// 4. Don't use with statement
with (obj) {  // Deprecated, strict mode error
    console.log(property);
}

// 5. Don't leave console.log in production
console.log('Debug info');  // Remove before deployment

// 6. Don't use == for comparison
0 == '0';     // true (coercion)
0 === '0';    // false (strict)

// 7. Don't ignore rejected promises
fetch('/api').then(data => { });  // Missing catch!

// 8. Don't use new Object(), new Array(), etc.
const obj = new Object();  // Use {}
const arr = new Array();   // Use []

// 9. Don't use undeclared variables
x = 10;  // Implicit global - bad!

// 10. Don't use magic numbers
if (status === 4) { }  // What is 4?
// Better:
const STATUS_COMPLETED = 4;
if (status === STATUS_COMPLETED) { }

// 11. Don't create functions in loops
for (let i = 0; i < 10; i++) {
    setTimeout(() => console.log(i), 100);  // All print 10!
}
// Fix with let (block-scoped) or IIFE

// 12. Don't rely on implicit coercion
const result = someVar + '';  // Be explicit: String(someVar)

// 13. Don't use arguments object
function bad() {
    console.log(arguments);  // Use rest parameters instead
}
function good(...args) {
    console.log(args);
}
```

### DRY Principle

**Definition:** DRY (Don't Repeat Yourself) is a software development principle stating that every piece of knowledge or logic should have a single, unambiguous representation in the codebase. Duplication leads to bugs when one copy is updated but others are not. Apply DRY by extracting repeated code into functions, using loops instead of copy-pasted blocks, and creating reusable modules.

```javascript
// Bad: Repeated code
function processUser(user) {
    if (user.status === 'active' && user.verified) {
        // ... process logic
    }
}

function deleteUser(user) {
    if (user.status === 'active' && user.verified) {
        // ... delete logic
    }
}

// Good: Extract common logic
function canModify(user) {
    return user.status === 'active' && user.verified;
}

function processUser(user) {
    if (!canModify(user)) return;
    // ... process logic
}

function deleteUser(user) {
    if (!canModify(user)) return;
    // ... delete logic
}

// Extract utilities
const formatCurrency = (amount, currency = 'USD') => {
    return new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency
    }).format(amount);
};

// Reuse everywhere
console.log(formatCurrency(100));      // $100.00
console.log(formatCurrency(100, 'EUR')); // €100.00
```

---

## 🔑 Key Takeaways

1. **Use const by default**, let when reassignment needed, never var
2. **Use strict equality (===)** to avoid type coercion bugs
3. **Handle asynchronous code** with async/await for readability
4. **Use array methods** (map, filter, reduce) over manual loops
5. **Always validate data** and handle errors gracefully
6. **Write modular code** using ES6 modules and functions
7. **Follow DRY principle** - extract reusable logic
8. **Use meaningful names** - code is read more than written

---

**Next:** Practice building projects to reinforce these concepts!
 