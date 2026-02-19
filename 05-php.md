# 🐘 PHP - PHP: Hypertext Preprocessor

## Summary

This document covers PHP, a server-side scripting language for web development. Topics include variables and data types, operators, control structures, functions, string and array manipulation, superglobals for handling HTTP requests, form processing and validation, file operations, sessions and cookies, error handling, PDO for database interactions, date/time handling, and code organization with includes.

## Sommaire

- [1. Introduction to PHP](#1-introduction-to-php)
  - [Definition](#definition)
  - [PHP Request/Response Architecture](#php-request/response-architecture)
  - [Basic Syntax & Request/Response Cycle](#basic-syntax-&-request/response-cycle)
  - [PHP Tags](#php-tags)
  - [Comments](#comments)
- [2. Variables & Data Types](#2-variables-&-data-types)
  - [Definition](#definition)
  - [Variable Scope Overview](#variable-scope-overview)
  - [Variable Declaration](#variable-declaration)
  - [Scalar Types](#scalar-types)
  - [Compound Types](#compound-types)
  - [Type Checking & Casting](#type-checking-&-casting)
  - [Constants](#constants)
- [3. Operators](#3-operators)
  - [Definition](#definition)
  - [Operator Categories Overview](#operator-categories-overview)
  - [Arithmetic Operators](#arithmetic-operators)
  - [Assignment Operators](#assignment-operators)
  - [Comparison Operators](#comparison-operators)
  - [Logical Operators](#logical-operators)
  - [String Operators](#string-operators)
  - [Null Coalescing & Ternary](#null-coalescing-&-ternary)
- [4. Control Structures](#4-control-structures)
  - [Definition](#definition)
  - [Control Flow Overview](#control-flow-overview)
  - [Conditional Statements](#conditional-statements)
  - [Switch Statement](#switch-statement)
  - [Loops](#loops)
  - [Break & Continue](#break-&-continue)
- [5. Functions](#5-functions)
  - [Definition](#definition)
  - [Function Scope and Lifecycle](#function-scope-and-lifecycle)
  - [Defining Functions](#defining-functions)
  - [Variable Scope](#variable-scope)
  - [Anonymous Functions & Closures](#anonymous-functions-&-closures)
  - [Arrow Functions (PHP 7.4+)](#arrow-functions-php-74+)
  - [Variadic Functions](#variadic-functions)
- [6. Strings](#6-strings)
  - [Definition](#definition)
  - [String Types and Interpolation](#string-types-and-interpolation)
  - [String Definition](#string-definition)
  - [String Functions](#string-functions)
  - [Multibyte String Functions](#multibyte-string-functions)
- [7. Arrays](#7-arrays)
  - [Definition](#definition)
  - [Array Types Hierarchy](#array-types-hierarchy)
  - [Creating Arrays](#creating-arrays)
  - [Array Operations](#array-operations)
  - [Array Functions (Functional Programming)](#array-functions-functional-programming)
  - [Array Destructuring](#array-destructuring)
- [8. Superglobals](#8-superglobals)
  - [Definition](#definition)
  - [Superglobals Reference](#superglobals-reference)
  - [$_GET](#$_get)
  - [$_POST](#$_post)
  - [$_REQUEST](#$_request)
  - [$_SERVER](#$_server)
  - [$_SESSION](#$_session)
  - [$_COOKIE](#$_cookie)
  - [$_FILES](#$_files)
  - [$_ENV](#$_env)
  - [$GLOBALS](#$globals)
- [9. Forms & Input Handling](#9-forms-&-input-handling)
  - [Definition](#definition)
  - [Form Submission Flow](#form-submission-flow)
  - [Processing Form Data](#processing-form-data)
  - [Input Sanitization & Validation](#input-sanitization-&-validation)
  - [CSRF Protection](#csrf-protection)
  - [File Uploads](#file-uploads)
- [10. Working with Files](#10-working-with-files)
  - [Definition](#definition)
  - [Reading Files](#reading-files)
  - [Writing Files](#writing-files)
  - [File Operations](#file-operations)
- [11. Sessions & Cookies](#11-sessions-&-cookies)
  - [Definition](#definition)
  - [Session Lifecycle](#session-lifecycle)
  - [Sessions](#sessions)
  - [Cookies](#cookies)
- [12. Error Handling](#12-error-handling)
  - [Definition](#definition)
  - [Error Handling Flow](#error-handling-flow)
  - [Error Types](#error-types)
  - [Exception Handling](#exception-handling)
  - [Custom Exceptions](#custom-exceptions)
- [13. Working with Databases (PDO)](#13-working-with-databases-pdo)
  - [Definition](#definition)
  - [PDO Prepared Statement Flow](#pdo-prepared-statement-flow)
  - [Connecting to Database](#connecting-to-database)
  - [Prepared Statements](#prepared-statements)
  - [Fetching Data](#fetching-data)
  - [CRUD Operations](#crud-operations)
  - [Transactions](#transactions)
- [14. Date & Time](#14-date-&-time)
  - [Definition](#definition)
  - [DateTime Object Lifecycle](#datetime-object-lifecycle)
  - [Date Functions](#date-functions)
  - [DateTime Class](#datetime-class)
- [15. Include/Require](#15-include/require)
  - [Definition](#definition)
  - [Include/Require Decision Flow](#include/require-decision-flow)
  - [Include vs Require](#include-vs-require)
  - [Autoloading](#autoloading)
  - [Project Structure](#project-structure)
- [🔑 Key Takeaways](#🔑-key-takeaways)



> A server-side scripting language designed for web development. PHP powers ~78% of all websites and excels at generating dynamic web content.

---

## 1. Introduction to PHP

### Definition
PHP is a server-side scripting language that executes on the web server before sending HTML to the browser. It can generate dynamic page content, handle forms, manage sessions, and interact with databases.

### PHP Request/Response Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    PHP WEB ARCHITECTURE                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   ┌──────────────┐          HTTP Request        ┌──────────┐    │
│   │              │ ────────────────────────────>│          │    │
│   │   Browser    │                              │  Web     │    │
│   │   (Client)   │ <────────────────────────────│  Server  │    │
│   │              │        HTTP Response         │          │    │
│   └──────────────┘                              └────┬─────┘    │
│          ▲                                           │          │
│          │                                           │          │
│          │    ┌──────────────────────────────────────┘          │
│          │    │                                                 │
│          │    ▼                                                 │
│          │    ┌─────────────┐                                   │
│          └─── │ PHP Engine  │                                   │
│               │  Executes   │                                   │
│               │  ┌────────┐ │                                   │
│               │  │ Parse  │ │                                   │
│               │  │ Compile│ │                                   │
│               │  │ Execute│ │                                   │
│               │  └────┬───┘ │                                   │
│               │       │     │                                   │
│               │       ▼     │                                   │
│               │  ┌────────┐ │                                   │
│               │  │Generate│ │                                   │
│               │  │ HTML   │ │                                   │
│               │  └────────┘ │                                   │
│               └─────────────┘                                   │
│                                                                 │
│   ┌────────────────────────────────────────────────────────┐    │
│   │ PHP Can Interact With:                                 │    │
│   │  • Databases (MySQL, PostgreSQL, SQLite)               │    │
│   │  • File System (read/write files)                      │    │
│   │  • External APIs (HTTP requests)                       │    │
│   │  • Session/Cookie storage                              │    │
│   │  • Email servers (SMTP)                                │    │
│   └────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────┘
```

### Basic Syntax & Request/Response Cycle

```php
<?php
// PHP code must be enclosed in <?php tags
// Everything outside these tags is sent as plain HTML

// This executes on the SERVER before HTML reaches the browser
echo "Hello, World!";

// PHP can be embedded in HTML
?>
<!DOCTYPE html>
<html>
<head>
    <title><?php echo "Dynamic Title"; ?></title>
</head>
<body>
    <h1>Welcome, <?php echo "User"; ?>!</h1>
    <p>Server time: <?php echo date('Y-m-d H:i:s'); ?></p>
</body>
</html>
```

**Request/Response Cycle:**
1. Browser sends request to server (e.g., `index.php`)
2. PHP interpreter executes PHP code on the server
3. PHP generates HTML output
4. Server sends pure HTML/CSS/JS to browser
5. Browser renders the page

```php
<?php
// Example: Server-side processing
$userName = "John";  // Data could come from database
$currentTime = date('H:i');
$isMorning = date('H') < 12;

// PHP generates different HTML based on conditions
if ($isMorning) {
    $greeting = "Good morning, $userName!";
} else {
    $greeting = "Good afternoon, $userName!";
}
?>
<!-- This HTML is sent to browser after PHP processing -->
<h1><?php echo $greeting; ?></h1>
<p>It's currently <?php echo $currentTime; ?></p>
```

### PHP Tags

**Definition:** PHP code is enclosed in strict start and end tags. The standard opening tag is `<?php` and the closing tag is `?>`. For files containing only PHP code, the closing tag `?>` is omitted (best practice) to prevent accidental whitespace output. Short echo tags `<?= ... ?>` are shorthand for `<?php echo ...; ?>`.

```php
<?php
// Standard PHP opening tag (always use this)
echo "Standard PHP";
?>

<?
// Short tags ( discouraged, depends on configuration)
// Avoid using - may be disabled on some servers
?>

<?=
// Short echo tag (safe to use since PHP 5.4)
<?= $variable ?>  // Equivalent to <?php echo $variable; ?>
?>
```

### Comments

**Definition:** Comments are non-executable lines used to document code. PHP supports C-style comments: `//` and `#` for single-line comments, and `/* ... */` for multi-line comments. PHPDoc comments `/** ... */` are a special standard for documenting classes, functions, and variables, recognized by IDEs and documentation generators.

```php
<?php
// Single-line comment

# Also a single-line comment (less common)

/*
 * Multi-line comment
 * Can span multiple lines
 */

/**
 * PHPDoc comment (for documentation)
 * @param string $name The user's name
 * @return string The greeting message
 */
function greet($name) {
    return "Hello, $name!";
}
?>
```

---

## 2. Variables & Data Types

### Definition
Variables in PHP start with `$` and are dynamically typed. PHP automatically determines the data type based on the assigned value. PHP supports scalar types (string, int, float, bool), compound types (array, object), and special types (null, resource).

### Variable Scope Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                    PHP VARIABLE SCOPE                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │                  GLOBAL SCOPE                        │      │
│  │  $globalVar = "accessible everywhere"                │      │
│  │                                                      │      │
│  │  ┌──────────────────────────────────────────┐       │      │
│  │  │            LOCAL SCOPE                   │       │      │
│  │  │  function myFunc() {                     │       │      │
│  │  │      $local = "only here";               │       │      │
│  │  │      // Access global:                   │       │      │
│  │  │      // global $globalVar;               │       │      │
│  │  │      // OR $GLOBALS['globalVar']         │       │      │
│  │  │  }                                       │       │      │
│  │  └──────────────────────────────────────────┘       │      │
│  │                                                      │      │
│  │  ┌──────────────────────────────────────────┐       │      │
│  │  │           STATIC SCOPE                   │       │      │
│  │  │  function counter() {                    │       │      │
│  │  │      static $count = 0;  // Persists     │       │      │
│  │  │      return ++$count;                    │       │      │
│  │  │  }                                       │       │      │
│  │  │  counter(); // 1                         │       │      │
│  │  │  counter(); // 2 (value remembered)      │       │      │
│  │  └──────────────────────────────────────────┘       │      │
│  └──────────────────────────────────────────────────────┘      │
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │              SUPERGLOBALS (Always Available)         │      │
│  │  $_GET, $_POST, $_SESSION, $_COOKIE, $_SERVER, ...   │      │
│  └──────────────────────────────────────────────────────┘      │
└─────────────────────────────────────────────────────────────────┘
```

### Variable Declaration

**Definition:** Variables in PHP start with a `$` sign followed by the name (e.g., `$variable`). They are dynamically typed (no type declaration needed), case-sensitive, and assigned by value (unless explicitly assigned by reference with `&`). Valid names must start with a letter or underscore.

```php
<?php
// Variables start with $ followed by a letter or underscore
$name = "John";           // String
$age = 25;               // Integer
$price = 19.99;          // Float
$isActive = true;        // Boolean
$nothing = null;         // Null

// Variable names are case-sensitive
$Name = "Jane";          // Different variable from $name

// Valid names
$_private = "value";
$userName = "john";      // camelCase (common)
$user_name = "john";     // snake_case
$UserName = "john";      // PascalCase (usually for classes)
?>
```

### Scalar Types

**Definition:** Scalar types represent a single value. PHP has four scalar types: `bool` (true/false), `int` (integers), `float` (floating-point numbers), and `string` (text). Since PHP 7, you can enforce these types in function signatures and return types (`function add(int $a, int $b): int`).

```php
<?php
// STRING - Text data
$greeting = "Hello, World!";
$name = 'John';
$combined = $greeting . " " . $name;  // String concatenation

// INTEGER - Whole numbers
$age = 25;
$negative = -10;
$large = PHP_INT_MAX;    // Platform dependent (usually 9223372036854775807)

// FLOAT (DOUBLE) - Decimal numbers
$price = 19.99;
$scientific = 1.23e4;    // 12300
$small = 1.23e-4;        // 0.000123

// Precision warning
$sum = 0.1 + 0.2;        // May not equal exactly 0.3 due to floating point

// BOOLEAN - true or false
$isLoggedIn = true;
$hasPermission = false;

// Everything converts to boolean
$bool1 = (bool) "";      // false (empty string)
$bool2 = (bool) "hello"; // true (non-empty string)
$bool3 = (bool) 0;       // false
$bool4 = (bool) 1;       // true
$bool5 = (bool) [];      // false (empty array)
$bool6 = (bool) [1,2];   // true (non-empty array)
$bool7 = (bool) null;    // false

// NULL - No value
$empty = null;
$unset;                  // Also null (but generates warning)
?>
```

### Compound Types

**Definition:** Compound types can hold multiple values. The two compound types in PHP are `array` (ordered map holding values with integer or string keys) and `object` (instance of a class). Additionally, `callable` (functions) and `iterable` (arrays or traversing objects) are pseudo-types used in type hinting.

```php
<?php
// ARRAY - Ordered map (can be used as list, map, stack, etc.)
// Indexed array (list)
$fruits = ["apple", "banana", "orange"];
$numbers = array(1, 2, 3, 4, 5);  // Old syntax

// Associative array (dictionary/map)
$user = [
    "name" => "John",
    "email" => "john@example.com",
    "age" => 25
];

// Multidimensional array
$matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

// OBJECT - Instance of a class
class Person {
    public $name;
    public $age;
    
    public function __construct($name, $age) {
        $this->name = $name;
        $this->age = $age;
    }
    
    public function greet() {
        return "Hello, I'm {$this->name}";
    }
}

$person = new Person("Alice", 30);
echo $person->name;      // "Alice"
echo $person->greet();   // "Hello, I'm Alice"

// CALLABLE - Functions that can be called
$callback = function($x) { return $x * 2; };
$functions = ['strpos', 'strlen'];
?>
```

### Type Checking & Casting

**Definition:** PHP provides functions like `gettype()`, `is_int()`, `is_string()`, etc., to check variable types at runtime. Type casting allows explicit conversion (e.g., `(int)$var`, `(string)$var`) to force a variable into a specific type. PHP also performs automatic type juggling (implicit coercion) in loose comparisons.

```php
<?php
$value = "42";

// Get type
gettype($value);              // "string"

// Type checking functions
is_string($value);            // true
is_int($value);               // false (it's a string)
is_numeric($value);           // true (can be converted to number)
is_array($value);             // false
is_object($value);            // false
is_null($value);              // false
is_bool($value);              // false
is_float($value);             // false
is_callable($value);          // false

// Type casting
$int = (int) "42";            // 42 (integer)
$float = (float) "3.14";      // 3.14 (float)
$string = (string) 42;        // "42" (string)
$bool = (bool) 1;             // true
$array = (array) "hello";     // ["hello"] (array with one element)

// Explicit type declarations (PHP 7+)
function add(int $a, int $b): int {
    return $a + $b;
}

// Union types (PHP 8+)
function process(string|int $input): string {
    return "Received: " . $input;
}

// Nullable types
function findUser(?int $id): ?array {
    if ($id === null) return null;
    // ... fetch from database
    return ["id" => $id, "name" => "John"];
}

// Type juggling (automatic conversion)
$sum = "5" + 3;               // 8 (string converted to int)
$concat = "5" . 3;            // "53" (int converted to string)
?>
```

### Constants

**Definition:** Constants are immutable values that cannot be changed once defined. They are defined using `define('NAME', value)` (global scope) or `const NAME = value` (class or global scope). Constants do not use the `$` prefix and are conventionally uppercase (e.g., `DB_HOST`, `API_KEY`).

```php
<?php
// Define constants (global scope, cannot be changed)
define("SITE_NAME", "My Website");
define("MAX_UPLOAD_SIZE", 1048576);  // 1MB in bytes
define("DB_HOST", "localhost");

// Constant arrays (PHP 7+)
define("ALLOWED_EXTENSIONS", ["jpg", "png", "gif"]);

// Using const keyword (for class constants or simple values)
const API_VERSION = "2.0";
const DEFAULT_LIMIT = 10;

// Class constants
class Config {
    const APP_NAME = "My App";
    const VERSION = "1.0.0";
    const DEBUG = true;
    
    // Visibility modifiers (PHP 7.1+)
    public const PUBLIC_CONST = "visible";
    private const PRIVATE_CONST = "hidden";
    protected const PROTECTED_CONST = "inherited";
}

echo Config::APP_NAME;        // "My App"
echo SITE_NAME;               // "My Website"

// Magic constants (automatically defined)
echo __LINE__;                // Current line number
echo __FILE__;                // Full path to current file
echo __DIR__;                 // Directory of current file
echo __FUNCTION__;            // Current function name
echo __CLASS__;               // Current class name
echo __METHOD__;              // Current class method name
echo __NAMESPACE__;           // Current namespace
echo __TRAIT__;               // Current trait name
echo ClassName::class;        // Fully qualified class name (PHP 5.5+)
?>
```

---

## 3. Operators

### Definition
Operators perform operations on variables and values. PHP supports arithmetic, assignment, comparison, logical, string, and other operators. Understanding operator precedence and the difference between loose (`==`) and strict (`===`) comparison is essential for writing bug-free code.

### Operator Categories Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                    PHP OPERATOR TYPES                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │ ARITHMETIC  │  │  ASSIGNMENT │  │  COMPARISON │             │
│  │             │  │             │  │             │             │
│  │ +  addition │  │ =   assign  │  │ ==  equal   │             │
│  │ -  subtract │  │ +=  add to  │  │ === identical│            │
│  │ *  multiply │  │ -=  sub from│  │ !=  not eq  │             │
│  │ /  divide   │  │ *=  mul by  │  │ !== not id  │             │
│  │ %  modulo   │  │ /=  div by  │  │ <   less    │             │
│  │ ** power    │  │ .=  concat  │  │ >   greater │             │
│  └─────────────┘  └─────────────┘  │ <=> spaceship│            │
│                                    └─────────────┘             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │   LOGICAL   │  │   STRING    │  │    OTHER    │             │
│  │             │  │             │  │             │             │
│  │ &&  AND     │  │ .  concat   │  │ ??  null coa│             │
│  │ ||  OR      │  │ .= append   │  │ ? : ternary │             │
│  │ !   NOT     │  │             │  │ @   suppress│             │
│  │ xor XOR     │  │             │  │ ``  exec    │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
│                                                                 │
│  ⚠️  CRITICAL: == vs ===                                        │
│      5 == "5"   → true  (loose comparison, type juggling)       │
│      5 === "5"  → false (strict comparison, same type)          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Arithmetic Operators

**Definition:** Arithmetic operators perform mathematical calculations: `+` (addition), `-` (subtraction), `*` (multiplication), `/` (division - returns float if needed), `%` (modulus), and `**` (exponentiation). PHP automatically converts types (e.g., strings to numbers) if possible during arithmetic operations.

```php
<?php
$a = 10;
$b = 3;

// Basic arithmetic
echo $a + $b;    // 13 (addition)
echo $a - $b;    // 7 (subtraction)
echo $a * $b;    // 30 (multiplication)
echo $a / $b;    // 3.333... (division)
echo $a % $b;    // 1 (modulo - remainder)
echo $a ** $b;   // 1000 (exponentiation - 10^3)

// Increment/Decrement
$count = 5;
echo ++$count;   // 6 (pre-increment: increment, then return)
echo $count++;   // 6 (post-increment: return, then increment)
echo --$count;   // 6 (pre-decrement)
echo $count--;   // 6 (post-decrement)

// Division by zero
$result = 10 / 0;  // Warning: Division by zero
?>
```

### Assignment Operators

**Definition:** Assignment operators assign values to variables. The basic assignment is `=`. Combined operators (`+=`, `-=`, `*=`, `/=`, `.=`) perform an operation and assignment in one step. Assignment by reference (`$a = &$b`) links variables so changes to one affect the other.

```php
<?php
$x = 10;         // Basic assignment

// Compound assignment
$x += 5;         // $x = $x + 5;  // 15
$x -= 3;         // $x = $x - 3;  // 12
$x *= 2;         // $x = $x * 2;  // 24
$x /= 4;         // $x = $x / 4;  // 6
$x %= 4;         // $x = $x % 4;  // 2
$x **= 3;        // $x = $x ** 3; // 8

// String concatenation assignment
$message = "Hello";
$message .= " World";  // "Hello World"

// Null coalescing assignment (PHP 7.4+)
$username = null;
$username ??= "guest";  // If $username is null, assign "guest"
?>
```

### Comparison Operators

```php
<?php
$a = 5;
$b = "5";
$c = 10;

// Equal (loose comparison - type juggling)
var_dump($a == $b);    // true (5 == 5 after type conversion)

// Identical (strict comparison - same type and value)
var_dump($a === $b);   // false (int !== string)
var_dump($a === 5);    // true

// Not equal
var_dump($a != $b);    // false
var_dump($a <> $b);    // false (alternative syntax)

// Not identical
var_dump($a !== $b);   // true

// Greater/Less than
var_dump($a > $c);     // false
var_dump($a < $c);     // true
var_dump($a >= 5);     // true
var_dump($a <= 5);     // true

// Spaceship operator (PHP 7+)
var_dump($a <=> $c);   // -1 (less than)
var_dump($c <=> $a);   // 1 (greater than)
var_dump($a <=> 5);    // 0 (equal)

// Useful for sorting
$numbers = [3, 1, 4, 1, 5];
usort($numbers, fn($a, $b) => $a <=> $b);

// Common gotchas
var_dump(true == "string");   // true (string converts to true)
var_dump(false == 0);         // true
var_dump(null == "");         // true
var_dump(null == 0);          // true

// Always use === for reliable comparisons
var_dump(true === "string");  // false
var_dump(false === 0);        // false
?>
```

### Logical Operators

**Definition:** Logical operators combine boolean expressions: `&&` / `and` (AND), `||` / `or` (OR), `!` (NOT), and `xor` (exclusive OR). `&&` and `||` have higher precedence than `and` and `or`. Like JavaScript, PHP uses short-circuit evaluation.

```php
<?php
$hasPermission = true;
$isLoggedIn = false;
$isAdmin = true;

// AND / && - both must be true
if ($isLoggedIn && $hasPermission) {
    echo "Access granted";
}

// OR / || - at least one must be true
if ($isLoggedIn || $isAdmin) {
    echo "Can view content";
}

// XOR - exactly one must be true (not both)
if ($isLoggedIn xor $isAdmin) {
    echo "Only one condition is true";
}

// NOT / ! - negation
if (!$isLoggedIn) {
    echo "Please log in";
}

// Short-circuit evaluation
function expensiveOperation() {
    echo "Expensive operation called";
    return true;
}

// && stops if first is false
false && expensiveOperation();  // Function not called

// || stops if first is true
true || expensiveOperation();   // Function not called

// Precedence: ! > && > ||
// Use parentheses for clarity
if (($isLoggedIn && $hasPermission) || $isAdmin) {
    // Clear intent
}
?>
```

### String Operators

**Definition:** PHP has two dedicated string operators: the concatenation operator `.` (dot) which joins two strings, and the concatenating assignment operator `.=` which appends the right string to the left variable. Unlike JavaScript, `+` is purely arithmetic in PHP — it adds, never concatenates.

```php
<?php
$first = "Hello";
$second = "World";

// Concatenation (.)
$greeting = $first . " " . $second;  // "Hello World"

// Concatenation assignment (.=)
$message = "Hello";
$message .= " ";
$message .= "PHP";                   // "Hello PHP"

// Variable interpolation in double quotes
$name = "John";
$greeting1 = "Hello, $name!";        // "Hello, John!"
$greeting2 = 'Hello, $name!';        // "Hello, $name!" (no interpolation)

// Complex interpolation
$object = new stdClass();
$object->name = "Jane";
echo "User: {$object->name}";        // "User: Jane"

$array = ["key" => "value"];
echo "Value: {$array['key']}";       // "Value: value"

// Heredoc (multiline with interpolation)
$text = <<<EOT
Hello, $name!
This is a multi-line string.
You can use "quotes" freely here.
EOT;

// Nowdoc (multiline without interpolation)
$code = <<<'EOT'
$name will not be interpolated.
This is literal text.
EOT;
?>
```

### Null Coalescing & Ternary

**Definition:** The **Ternary Operator** (`? :`) evaluates a condition and returns one of two values. The **Null Coalescing Operator** (`??`) returns the left operand if it exists and is not null; otherwise, it returns the right operand. The **Spaceship Operator** (`<=>`) returns -1, 0, or 1 for comparisons (less than, equal, greater than).

```php
<?php
$user = null;
$name = "John";

// Null coalescing (??) - returns first non-null value
echo $user ?? "Guest";        // "Guest" ($user is null)
echo $name ?? "Unknown";      // "John" ($name has value)

// Chaining null coalescing
echo $user ?? $name ?? "Anonymous";  // "John"

// Null coalescing assignment (PHP 7.4+)
$count = null;
$count ??= 0;                 // $count is 0 (only assigns if null)
$count ??= 10;                // $count stays 0 (not null)

// Nullsafe operator (PHP 8+ - ?->)
$user = getUser();  // Could return null or object
$country = $user?->address?->country;  // null if any is null, no error

// Ternary operator (condition ? true : false)
$status = $age >= 18 ? "adult" : "minor";

// Shorthand ternary (PHP 5.3+)
$result = $input ?: "default";  // If $input is truthy, use it, else "default"

// Nested ternary (use parentheses for clarity)
$category = $age < 13 ? "child" : ($age < 20 ? "teen" : "adult");
?>
```

---

## 4. Control Structures

### Definition
Control structures determine the flow of program execution based on conditions and loops. PHP provides conditional statements (if, switch, match), looping constructs (for, while, foreach), and control flow statements (break, continue) to manage program logic.

### Control Flow Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                 CONTROL STRUCTURE FLOW                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │                  CONDITIONALS                        │      │
│  │                                                      │      │
│  │   ┌──────────┐    ┌──────────┐    ┌──────────┐      │      │
│  │   │    IF    │    │  SWITCH  │    │   MATCH  │      │      │
│  │   │          │    │          │    │ (PHP 8+) │      │      │
│  │   │ if (cond)│    │ switch($x│    │ match($x)│      │      │
│  │   │   stmt;  │    │ { case 1:│    │ {        │      │      │
│  │   │ elseif() │    │   ...    │    │  1 => a, │      │      │
│  │   │   stmt;  │    │ case 2:  │    │  2 => b, │      │      │
│  │   │ else     │    │   ...    │    │  default │      │      │
│  │   │   stmt;  │    │ }        │    │    => c  │      │      │
│  │   └──────────┘    └──────────┘    └──────────┘      │      │
│  └──────────────────────────────────────────────────────┘      │
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │                    LOOPS                             │      │
│  │                                                      │      │
│  │   ┌──────────┐    ┌──────────┐    ┌──────────┐      │      │
│  │   │   FOR    │    │  WHILE   │    │ FOREACH  │      │      │
│  │   │          │    │          │    │          │      │      │
│  │   │ for($i=0 │    │ while()  │    │ foreach()│      │      │
│  │   │   ;$i<10 │    │ {        │    │ {        │      │      │
│  │   │   ;$i++) │    │   stmt;  │    │   stmt;  │      │      │
│  │   │ {        │    │ }        │    │ }        │      │      │
│  │   │   stmt;  │    │          │    │          │      │      │
│  │   │ }        │    │          │    │          │      │      │
│  │   └──────────┘    └──────────┘    └──────────┘      │      │
│  │                                                      │      │
│  │   Use FOR when:      Use WHILE when:   Use FOREACH: │      │
│  │   • Known iterations • Unknown count    • Arrays     │      │
│  │   • Counter needed   • Condition-based  • Iterables  │      │
│  └──────────────────────────────────────────────────────┘      │
└─────────────────────────────────────────────────────────────────┘
```

### Conditional Statements

**Definition:** Conditional statements control the flow of execution based on boolean conditions. The primary structure is `if`, `elseif`, and `else`. PHP also supports the alternative syntax (`if (...): ... endif;`) often used in templates. Conditions mimic C-style syntax and support both loose and strict comparisons.

```php
<?php
$age = 25;
$isMember = true;

// if statement
if ($age >= 18) {
    echo "You are an adult";
}

// if-else
if ($age >= 18) {
    echo "Adult";
} else {
    echo "Minor";
}

// if-elseif-else
if ($age < 13) {
    echo "Child";
} elseif ($age < 20) {
    echo "Teenager";
} elseif ($age < 65) {
    echo "Adult";
} else {
    echo "Senior";
}

// Alternative syntax (good for templates)
if ($isMember): ?>
    <p>Welcome back, member!</p>
<?php else: ?>
    <p>Please sign up to become a member.</p>
<?php endif; ?>

// Multiple conditions
if ($age >= 18 && $isMember) {
    echo "Welcome, adult member!";
}

// Ternary for simple conditions
echo $age >= 18 ? "Adult" : "Minor";

// Null coalescing for defaults
$username = $_GET['user'] ?? 'Guest';

// Using match expression (PHP 8+)
$status = match($age) {
    0, 1, 2 => 'baby',
    3, 4, 5 => 'toddler',
    6, 7, 8, 9, 10, 11, 12 => 'child',
    default => match(true) {
        $age < 20 => 'teenager',
        $age < 65 => 'adult',
        default => 'senior'
    }
};
?>
```

### Switch Statement

**Definition:** The `switch` statement compares a variable against multiple values (`case`). It executes the code block associated with the first matching case. Unlike `if/elseif`, switch performs loose comparison (`==`) by default. The `match` expression (introduced in PHP 8.0) provides a stricter, more concise alternative that returns a value.

```php
<?php
$day = "Monday";

// Switch statement
switch ($day) {
    case "Monday":
        echo "Start of work week";
        break;  // Don't forget break!
    case "Tuesday":
    case "Wednesday":
    case "Thursday":
        echo "Midweek";
        break;
    case "Friday":
        echo "Almost weekend!";
        break;
    case "Saturday":
    case "Sunday":
        echo "Weekend!";
        break;
    default:
        echo "Invalid day";
}

// Alternative syntax
switch ($day):
    case "Monday":
        echo "Monday blues";
        break;
endswitch;

// Match expression (PHP 8+) - more concise and returns value
$result = match($day) {
    "Monday" => "Start of work week",
    "Tuesday", "Wednesday", "Thursday" => "Midweek",
    "Friday" => "Almost weekend!",
    "Saturday", "Sunday" => "Weekend!",
    default => "Invalid day"
};

// Match with conditions
$score = 85;
$grade = match(true) {
    $score >= 90 => 'A',
    $score >= 80 => 'B',
    $score >= 70 => 'C',
    $score >= 60 => 'D',
    default => 'F'
};
?>
```

### Loops

**Definition:** Loops repeatedly execute a block of code. PHP supports four types: `for` (standard counter loop), `while` (condition checked before), `do-while` (condition checked after), and `foreach` (specialized for iterating over arrays and objects). `foreach` is the most common loop in PHP application code.

```php
<?php
// FOR loop - when you know the count
for ($i = 0; $i < 5; $i++) {
    echo "Iteration: $i\n";
}

// Multiple expressions
for ($i = 0, $j = 10; $i < 10; $i++, $j--) {
    echo "i: $i, j: $j\n";
}

// Infinite loop with break
for (;;) {
    if (shouldStop()) break;
}

// WHILE loop - condition checked before each iteration
$count = 0;
while ($count < 5) {
    echo "Count: $count\n";
    $count++;
}

// DO-WHILE loop - executes at least once
$num = 5;
do {
    echo "Number: $num\n";
    $num++;
} while ($num < 5);  // Executes once even though condition is false

// FOREACH loop - iterate over arrays
$colors = ["red", "green", "blue"];

// Indexed array
foreach ($colors as $color) {
    echo "Color: $color\n";
}

// With index
foreach ($colors as $index => $color) {
    echo "$index: $color\n";
}

// Associative array
$user = ["name" => "John", "age" => 30, "city" => "NYC"];
foreach ($user as $key => $value) {
    echo "$key: $value\n";
}

// Modifying values by reference (&)
$numbers = [1, 2, 3, 4, 5];
foreach ($numbers as &$num) {
    $num *= 2;  // Modifies original array
}
unset($num);  // Important: unset reference after loop

// Alternative syntax (good for templates)
foreach ($users as $user): ?>
    <div><?= htmlspecialchars($user['name']) ?></div>
<?php endforeach; ?>
?>
```

### Break & Continue

**Definition:** `break` ends execution of the current `for`, `foreach`, `while`, `do-while`, or `switch` structure. `continue` skips the rest of the current loop iteration and continues execution at the condition evaluation/incrementor. Both accept an optional numeric argument to break/continue out of multiple nested levels.

```php
<?php
// BREAK - exit loop immediately
for ($i = 0; $i < 10; $i++) {
    if ($i == 5) {
        break;  // Exit loop when $i reaches 5
    }
    echo $i;  // Outputs: 01234
}

// BREAK with levels (exit nested loops)
for ($i = 0; $i < 3; $i++) {
    for ($j = 0; $j < 3; $j++) {
        if ($j == 1) {
            break 2;  // Break out of both loops
        }
        echo "i:$i j:$j ";
    }
}

// CONTINUE - skip to next iteration
for ($i = 0; $i < 10; $i++) {
    if ($i % 2 == 0) {
        continue;  // Skip even numbers
    }
    echo $i;  // Outputs: 13579
}

// CONTINUE with levels
foreach ($matrix as $row) {
    foreach ($row as $cell) {
        if ($cell === null) {
            continue 2;  // Skip to next row
        }
        process($cell);
    }
}

// GOTO (avoid using - hard to follow)
for ($i = 0; $i < 10; $i++) {
    if ($i == 5) {
        goto end;  // Jump to label
    }
    echo $i;
}
end:
echo "Loop ended";
?>
```

---

## 5. Functions

### Definition
Functions are reusable blocks of code that perform specific tasks. PHP has built-in functions and supports user-defined functions with features like type declarations, default parameters, variadic arguments, and anonymous functions/closures.

### Function Scope and Lifecycle

```
┌─────────────────────────────────────────────────────────────────┐
│                   PHP FUNCTION TYPES                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │              NAMED FUNCTIONS                         │      │
│  │                                                      │      │
│  │  function add(int $a, int $b): int {                 │      │
│  │      return $a + $b;                                 │      │
│  │  }                                                   │      │
│  │                                                      │      │
│  │  ├─ Parameters: Input values                         │      │
│  │  ├─ Return Type: Output type declaration             │      │
│  │  ├─ Scope: Local by default                          │      │
│  │  └─ Visibility: Can access globals via 'global'      │      │
│  └──────────────────────────────────────────────────────┘      │
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │           ANONYMOUS FUNCTIONS (CLOSURES)             │      │
│  │                                                      │      │
│  │  $greet = function($name) use ($prefix) {            │      │
│  │      return "$prefix, $name!";                      │      │
│  │  };                                                  │      │
│  │                                                      │      │
│  │  ├─ Assigned to variables                            │      │
│  │  ├─ 'use' captures parent scope variables            │      │
│  │  └─ Often used as callbacks                          │      │
│  └──────────────────────────────────────────────────────┘      │
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │           ARROW FUNCTIONS (PHP 7.4+)                 │      │
│  │                                                      │      │
│  │  $double = fn($x) => $x * 2;                         │      │
│  │                                                      │      │
│  │  ├─ Concise single-expression syntax                 │      │
│  │  └─ Auto-captures variables from parent scope        │      │
│  └──────────────────────────────────────────────────────┘      │
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │              VARIADIC FUNCTIONS                      │      │
│  │                                                      │      │
│  │  function sum(...$numbers): int {                    │      │
│  │      return array_sum($numbers);                     │      │
│  │  }                                                   │      │
│  │  sum(1, 2, 3, 4, 5);  // Any number of args          │      │
│  └──────────────────────────────────────────────────────┘      │
└─────────────────────────────────────────────────────────────────┘
```

### Defining Functions

**Definition:** A function is a named block of code that performs a specific task. Functions are defined using the `function` keyword. In PHP, functions are part of the global scope (unless they are methods inside a class) and can be called before they are defined (except when conditionally defined).

```php
<?php
// Basic function
function greet() {
    echo "Hello, World!";
}
greet();

// Function with parameters
function greetUser($name) {
    echo "Hello, $name!";
}
greetUser("Alice");  // "Hello, Alice!"

// Function with return value
function add($a, $b) {
    return $a + $b;
}
$sum = add(5, 3);  // 8

// Multiple return statements
function getStatus($code) {
    if ($code == 200) {
        return "OK";
    } elseif ($code == 404) {
        return "Not Found";
    }
    return "Unknown";
}

// Returning multiple values (as array)
function getMinMax($numbers) {
    return [min($numbers), max($numbers)];
}
list($min, $max) = getMinMax([3, 1, 4, 1, 5]);  // $min=1, $max=5
// Or using array destructuring (PHP 7.1+)
[$min, $max] = getMinMax([3, 1, 4, 1, 5]);

// Type declarations (PHP 7+)
function multiply(int $a, int $b): int {
    return $a * $b;
}

// Union types (PHP 8+)
function formatInput(string|int $input): string {
    return (string) $input;
}

// Nullable types
function findUser(?int $id): ?array {
    if ($id === null) return null;
    // ... fetch user
    return ["id" => $id, "name" => "John"];
}

// Default parameter values
function greetWithTitle($name, $title = "Mr.") {
    return "Hello, $title $name";
}
echo greetWithTitle("Smith");           // "Hello, Mr. Smith"
echo greetWithTitle("Doe", "Dr.");      // "Hello, Dr. Doe"

// Default values must be after required parameters
function createUser($name, $email, $active = true, $role = "user") {
    // Valid - defaults at the end
}

// Pass-by-reference (&)
function doubleValue(&$number) {
    $number *= 2;
}
$value = 5;
doubleValue($value);
echo $value;  // 10 (original variable modified)

// Strict typing
declare(strict_types=1);  // Must be first statement in file
function addStrict(int $a, int $b): int {
    return $a + $b;
}
// addStrict("5", "3");  // TypeError!
?>
```

### Variable Scope

**Definition:** Variable scope determines where variables are accessible. PHP has two main scopes: **global** (outside functions) and **local** (inside functions). Unlike JavaScript, global variables are NOT automatically available inside functions — you must import them with the `global` keyword. Superglobals (`$_GET`, etc.) are exceptions and are available everywhere.

```php
<?php
$globalVar = "I'm global";

function testScope() {
    // Cannot access $globalVar here directly
    // echo $globalVar;  // Error: Undefined variable
    
    // Access global variable with 'global' keyword
    global $globalVar;
    echo $globalVar;
    
    // Or use $GLOBALS superglobal
    echo $GLOBALS['globalVar'];
}

// Static variables (persist between calls)
function counter() {
    static $count = 0;  // Initialized only once
    $count++;
    return $count;
}
echo counter();  // 1
echo counter();  // 2
echo counter();  // 3

// Function parameters have local scope
function example($param) {
    // $param is local to this function
    $local = "local variable";
}

// Anonymous functions and closures
$greeting = function($name) {
    return "Hello, $name";
};
echo $greeting("World");

// Closures with 'use' keyword (capture variables from parent scope)
$prefix = "Hello";
$sayHello = function($name) use ($prefix) {
    return "$prefix, $name!";
};
echo $sayHello("Alice");  // "Hello, Alice!"

// Capture by reference
$count = 0;
$increment = function() use (&$count) {
    $count++;
};
$increment();
$increment();
echo $count;  // 2
?>
```

### Anonymous Functions & Closures

**Definition:** Anonymous functions (closures) are functions without a name, useful for callbacks and inline logic. A closure captures variables from the parent scope using the `use` keyword. They are objects of the `Closure` class and can be assigned to variables or passed as arguments.

```php
<?php
// Anonymous function assigned to variable
$square = function($n) {
    return $n * $n;
};
echo $square(4);  // 16

// Using as callback
$numbers = [1, 2, 3, 4, 5];
$squared = array_map(function($n) {
    return $n * $n;
}, $numbers);

// Closure with 'use'
$multiplier = 3;
$multiply = function($n) use ($multiplier) {
    return $n * $multiplier;
};
echo $multiply(5);  // 15

// Closure class (converting callable to object)
$closure = function($a, $b) { return $a + $b; };
echo $closure(2, 3);  // 5

// Bind closure to object scope
class Counter {
    private $count = 0;
    
    public function getIncrementer() {
        return function() {
            return ++$this->count;  // Accesses private property
        };
    }
}

$counter = new Counter();
$increment = $counter->getIncrementer();
echo $increment();  // 1
echo $increment();  // 2
?>
```

### Arrow Functions (PHP 7.4+)

**Definition:** Arrow functions (`fn($args) => expression`) provide a concise syntax for anonymous functions. They fundamentally differ from standard anonymous functions in that they **automatically capture variables** from the parent scope by value (no `use` keyword needed) and contain only a single expression which is automatically returned.

```php
<?php
// Basic arrow function
$double = fn($x) => $x * 2;
echo $double(5);  // 10

// Multiple parameters
$add = fn($a, $b) => $a + $b;
echo $add(3, 4);  // 7

// Arrow functions automatically capture variables
$factor = 10;
$multiply = fn($x) => $x * $factor;  // $factor captured automatically
echo $multiply(5);  // 50

// With array functions
$numbers = [1, 2, 3, 4, 5];
$doubled = array_map(fn($n) => $n * 2, $numbers);
$evens = array_filter($numbers, fn($n) => $n % 2 === 0);
$sum = array_reduce($numbers, fn($carry, $n) => $carry + $n, 0);

// In associative array operations
$users = [
    ['name' => 'John', 'age' => 30],
    ['name' => 'Jane', 'age' => 25],
];
$names = array_map(fn($user) => $user['name'], $users);
$adults = array_filter($users, fn($user) => $user['age'] >= 18);

// Limitations: only single expression, no statements
// This won't work:
// $complex = fn($x) => { echo $x; return $x * 2; };
?>
```

### Variadic Functions

**Definition:** Variadic functions accept a variable number of arguments using the strictly typed `...$args` operator (splat operator). This collects excess arguments into an array. Conversely, the splat operator can unpack an array into individual arguments when calling a function.

```php
<?php
// Variadic function (... operator)
function sum(...$numbers) {
    $total = 0;
    foreach ($numbers as $num) {
        $total += $num;
    }
    return $total;
}

echo sum(1, 2, 3);           // 6
echo sum(10, 20);            // 30
echo sum();                  // 0 (no arguments)

// Variadic with type hints
function concat(string ...$strings): string {
    return implode(" ", $strings);
}
echo concat("Hello", "World", "!");  // "Hello World !"

// Combining regular and variadic parameters
function formatMessage($template, ...$values) {
    return vsprintf($template, $values);
}
echo formatMessage("Hello, %s! You have %d messages.", "Alice", 5);

// Spread operator (splat) when calling functions
$nums = [1, 2, 3, 4, 5];
echo sum(...$nums);  // Unpacks array as arguments

// Named arguments (PHP 8+)
function createUser($name, $email, $age = null, $active = true) {
    return compact('name', 'email', 'age', 'active');
}

// Can skip optional parameters
$user = createUser(
    email: "john@example.com",
    name: "John",
    active: false
);

// Combine positional and named (positional must come first)
$user2 = createUser("Jane", "jane@example.com", active: true);
?>
```

---

## 6. Strings

### Definition
Strings are sequences of characters. PHP offers powerful string manipulation functions and multiple ways to define strings including single quotes, double quotes, heredoc, and nowdoc syntax. PHP provides extensive functions for searching, replacing, formatting, and manipulating strings.

### String Types and Interpolation

**Definition:** In PHP, strings can be defined using single quotes (`'`), double quotes (`"`), heredoc (`<<<`), or nowdoc (`<<<'`). Double quotes and heredoc support **variable interpolation** (parsing variables inside the string) and escape sequences (`\n`, `\t`). Single quotes and nowdoc treat the content literally.

```
┌─────────────────────────────────────────────────────────────────┐
│                    PHP STRING TYPES                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │              SINGLE QUOTES ''                        │      │
│  │                                                      │      │
│  │  'Hello $name'  →  Hello $name    (literal)          │      │
│  │  'It\'s fine'  →  It's fine      (escape \')         │      │
│  │                                                      │      │
│  │  ✓ Fastest, no parsing                               │      │
│  │  ✗ No variable interpolation                         │      │
│  └──────────────────────────────────────────────────────┘      │
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │              DOUBLE QUOTES ""                        │      │
│  │                                                      │      │
│  │  "Hello $name"    →  Hello John    (interpolated)    │      │
│  │  "Hello {$obj->name}"  (complex)                     │      │
│  │  "Line 1\nLine 2"  →  Supports escape sequences       │      │
│  │                                                      │      │
│  │  ✓ Variable interpolation                            │      │
│  │  ✓ Escape sequences (\n, \t, \u{}, etc.)             │      │
│  └──────────────────────────────────────────────────────┘      │
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │              HEREDOC <<<EOF                          │      │
│  │                                                      │      │
│  │  $text = <<<EOF                                      │      │
│  │  Hello, $name!                                       │      │
│  │  This is multi-line with "quotes"                    │      │
│  │  EOF;                                                │      │
│  │                                                      │      │
│  │  ✓ Multi-line with interpolation                     │      │
│  └──────────────────────────────────────────────────────┘      │
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │              NOWDOC <<<'EOF'                         │      │
│  │                                                      │      │
│  │  $text = <<<'EOF'                                    │      │
│  │  Hello, $name!  →  Literal $name                     │      │
│  │  EOF;                                                │      │
│  │                                                      │      │
│  │  ✓ Multi-line, no interpolation                      │      │
│  │  ✓ Like single quotes for multiple lines             │      │
│  └──────────────────────────────────────────────────────┘      │
└─────────────────────────────────────────────────────────────────┘
```

### String Definition

```php
<?php
// Single quotes - literal text (no variable interpolation)
$name = 'John';
$greeting = 'Hello, $name';  // "Hello, $name" (literal)
$escaped = 'It\'s a nice day';  // Need to escape single quotes

// Double quotes - variable interpolation and escape sequences
$greeting = "Hello, $name";     // "Hello, John"
$greeting2 = "Hello, {$name}!"; // "Hello, John!" (braces for clarity)
$multiline = "Line 1\nLine 2\tTabbed";  // \n = newline, \t = tab

// Escape sequences in double quotes
$examples = "
\\    - Backslash
\$   - Dollar sign
\"   - Double quote
\n   - Newline
\r   - Carriage return
\t   - Tab
\x0A - Hex character
\u{00A9} - Unicode (©)
";

// Heredoc (multiline with interpolation)
$name = "Alice";
$text = <<<EOT
Hello, $name!
This is a multi-line string.
You can use "quotes" and 'apostrophes' freely.
Variables like {$name} work here.
EOT;

// Nowdoc (multiline without interpolation)
$literal = <<<'EOT'
This is literal text.
$name will NOT be interpolated.
No escape sequences either.
EOT;

// Complex variable interpolation
$array = ["key" => "value"];
$object = new stdClass();
$object->property = "data";

echo "Array: {$array['key']}\n";
echo "Object: {$object->property}\n";
?>
```

### String Functions

**Definition:** PHP provides a vast library of built-in functions for string manipulation. Common operations include getting length (`strlen`), searching (`strpos`), extracting substrings (`substr`), replacing (`str_replace`), splitting (`explode`), and trimming whitespace (`trim`). Note that standard string functions are not multibyte-safe.

```php
<?php
$string = "Hello, World!";

// Length and position
strlen($string);                    // 13 (byte count)
mb_strlen($string, 'UTF-8');        // 13 (character count, multibyte safe)
strpos($string, "World");           // 7 (position, 0-indexed)
strpos($string, "world");           // false (case-sensitive)
stripos($string, "world");          // 7 (case-insensitive)
strrpos($string, "o");              // 8 (last occurrence)

// Substring extraction
substr($string, 0, 5);              // "Hello" (start, length)
substr($string, 7);                 // "World!" (from position to end)
substr($string, -6);                // "World!" (6 chars from end)
substr($string, -6, 3);             // "Wor"

// String replacement
str_replace("World", "PHP", $string);        // "Hello, PHP!"
str_replace(["Hello", "World"], ["Hi", "PHP"], $string);  // "Hi, PHP!"
str_ireplace("world", "PHP", $string);       // Case-insensitive

// Replace limited occurrences
str_replace("l", "L", $string, $count);      // $count = 3

// String manipulation
strtolower($string);                // "hello, world!"
strtoupper($string);                // "HELLO, WORLD!"
ucfirst("hello");                   // "Hello"
lcfirst("Hello");                   // "hello"
ucwords("hello world");             // "Hello World"

// Trimming
$dirty = "  hello world  ";
trim($dirty);                       // "hello world" (both ends)
ltrim($dirty);                      // "hello world  " (left only)
rtrim($dirty);                      // "  hello world" (right only)
trim($dirty, " h");                 // "ello world" (custom characters)

// Padding
str_pad("5", 3, "0", STR_PAD_LEFT);     // "005"
str_pad("5", 3, "0", STR_PAD_RIGHT);    // "500"
str_pad("5", 3, "0", STR_PAD_BOTH);     // "050"

// Repeating and reversing
str_repeat("*", 10);                // "**********"
strrev($string);                    // "!dlroW ,olleH"

// Comparison
strcmp("abc", "def");               // < 0 (abc comes before def)
strcmp("abc", "abc");               // 0 (equal)
strcasecmp("ABC", "abc");           // 0 (case-insensitive)

// String splitting
$parts = explode(",", "a,b,c");     // ["a", "b", "c"]
$parts = str_split("hello", 2);     // ["he", "ll", "o"]
$chars = str_split("hello");        // ["h", "e", "l", "l", "o"]

// Joining arrays
implode(",", ["a", "b", "c"]);      // "a,b,c"
join(" - ", ["apple", "banana"]);   // "apple - banana"

// Formatting
sprintf("Hello, %s! You have %d messages.", "Alice", 5);
// "Hello, Alice! You have 5 messages."

// Format specifiers
printf("Pi is %.2f", 3.14159);      // "Pi is 3.14"
printf("|%10s|", "right");          // "|     right|" (right-aligned)
printf("|%-10s|", "left");           // "|left      |" (left-aligned)
printf("|%010d|", 42);              // "|0000000042|" (zero-padded)
printf("|%'.10d|", 42);             // "|........42|" (custom padding)

// Number formatting
number_format(1234567.89);          // "1,234,568" (default rounding)
number_format(1234567.89, 2);       // "1,234,567.89"
number_format(1234567.89, 2, ",", ".");  // European format

// Hashing
md5("password");                    // MD5 hash (32 chars) - NOT for passwords
sha1("password");                   // SHA1 hash (40 chars) - NOT for passwords
password_hash("password", PASSWORD_DEFAULT);  // Secure password hashing
?>
```

### Multibyte String Functions

**Definition:** Multibyte string functions (prefixed with `mb_`) are required when working with Unicode characters (like UTF-8) where a single character may take more than one byte. Standard functions like `strlen()` count bytes, not characters. Always use `mb_strlen()`, `mb_substr()`, etc., when handling user input or localized content.

```php
<?php
// For UTF-8 and other multibyte encodings, use mb_* functions
$utf8String = "Hello 世界";  // Mixed ASCII and Chinese

// Wrong (counts bytes)
strlen($utf8String);                // 12 (some characters are multi-byte)

// Right (counts characters)
mb_strlen($utf8String, 'UTF-8');    // 8 (actual characters)

// Other mb functions
mb_substr($utf8String, 6, 2);       // "世界" (correct character positions)
mb_strpos($utf8String, "世");       // 6
mb_strtolower($utf8String);         // "hello 世界"
mb_strtoupper($utf8String);         // "HELLO 世界"

// Encoding conversion
mb_convert_encoding($string, 'UTF-8', 'ISO-8859-1');

// Detect encoding
mb_detect_encoding($string);

// Internal encoding
mb_internal_encoding('UTF-8');      // Set default encoding
?>
```

---

## 7. Arrays

### Definition
Arrays in PHP are ordered maps that can be used as lists, dictionaries, stacks, queues, and more. PHP arrays are versatile data structures that can store multiple values under a single variable name, with support for indexed, associative, and multidimensional structures.

### Array Types Hierarchy

```
┌─────────────────────────────────────────────────────────────────┐
│                   PHP ARRAY TYPES                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                    ┌───────────────┐                           │
│                    │  PHP ARRAY    │                           │
│                    │ (Ordered Map) │                           │
│                    └───────┬───────┘                           │
│                            │                                   │
│           ┌────────────────┼────────────────┐                  │
│           │                │                │                  │
│           ▼                ▼                ▼                  │
│    ┌────────────┐   ┌────────────┐   ┌────────────┐           │
│    │  INDEXED   │   │ ASSOCIATIVE│   │MULTIDIMEN- │           │
│    │   ARRAY    │   │   ARRAY    │   │  SIONAL    │           │
│    │            │   │            │   │   ARRAY    │           │
│    ├────────────┤   ├────────────┤   ├────────────┤           │
│    │ $arr[0]    │   │ $arr['key']│   │ $arr[0][0] │           │
│    │ $arr[1]    │   │ $arr['id'] │   │ $arr[1][2] │           │
│    │ $arr[2]    │   │ $arr['name│   │ Nested     │           │
│    │            │   │            │   │ arrays     │           │
│    └────────────┘   └────────────┘   └────────────┘           │
│                                                                 │
│    $fruits =        $user =          $matrix =                 │
│    [                [                [                         │
│      "apple",        "name" =>       [1, 2, 3],               │
│      "banana",       "John",         [4, 5, 6],               │
│      "orange"        "age" => 25     [7, 8, 9]                │
│    ];               ];             ];                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Creating Arrays

**Definition:** An array in PHP is actually an ordered map that maps values to keys. Arrays can be indexed (integer keys, 0-based by default) or associative (string keys). They are dynamic and can hold values of different types. Use the short array syntax `[]` (preferred) or `array()`.

```php
<?php
// Indexed arrays (lists)
$fruits = ["apple", "banana", "orange"];
$numbers = array(1, 2, 3, 4, 5);  // Old syntax

// Associative arrays (key-value pairs)
$user = [
    "name" => "John",
    "email" => "john@example.com",
    "age" => 25
];

// Mixed arrays (not recommended, but possible)
$mixed = ["first", "name" => "John", "second", 10 => "tenth"];
// Keys: 0, "name", 1, 10

// Empty array
$empty = [];
$alsoEmpty = array();

// Array with range
$oneToTen = range(1, 10);           // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
$letters = range('a', 'z');         // ['a', 'b', ..., 'z']
$evens = range(0, 10, 2);           // [0, 2, 4, 6, 8, 10]

// Multidimensional arrays
$matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

echo $matrix[1][2];  // 6 (row 1, column 2)

// Array of objects/associative arrays
$users = [
    ["id" => 1, "name" => "John"],
    ["id" => 2, "name" => "Jane"],
    ["id" => 3, "name" => "Bob"]
];

// Accessing elements
echo $fruits[0];        // "apple"
echo $user["name"];     // "John"

// Checking if key exists
isset($user["name"]);           // true
isset($user["phone"]);          // false
array_key_exists("name", $user); // true (works even if value is null)
?>
```

### Array Operations

**Definition:** Common array operations include accessing elements by key (`$arr['key']`), adding elements (`$arr[] = 'val'`), removing elements (`unset()`), counting elements (`count()`), and checking for keys (`array_key_exists`) or values (`in_array`). Arrays are passed by value by default, so modifying a copy doesn't affect the original unless passed by reference.

```php
<?php
$fruits = ["apple", "banana"];

// Adding elements
$fruits[] = "orange";               // Append
array_push($fruits, "grape");       // Push (add to end)
array_unshift($fruits, "mango");    // Unshift (add to beginning)

// Removing elements
$last = array_pop($fruits);         // Remove and return last
$first = array_shift($fruits);      // Remove and return first

// Array length
count($fruits);                     // Number of elements
sizeof($fruits);                    // Alias of count()

// Checking emptiness
empty($fruits);                     // true if empty
!empty($fruits);                    // true if has elements

// Slicing
$slice = array_slice($fruits, 1, 2);     // Elements 1 and 2
$slice = array_slice($fruits, -2);       // Last 2 elements

// Splicing (modify array)
array_splice($fruits, 1, 1);             // Remove 1 element at index 1
array_splice($fruits, 1, 0, "kiwi");     // Insert at index 1
array_splice($fruits, 1, 1, ["a", "b"]); // Replace with multiple

// Searching
in_array("apple", $fruits);              // true
array_search("apple", $fruits);          // 0 (index)
array_key_exists("name", $user);         // true

// Sorting
sort($numbers);                          // Sort ascending (re-indexes)
rsort($numbers);                         // Sort descending
asort($user);                            // Sort by value, keep keys
arsort($user);                           // Sort by value descending, keep keys
ksort($user);                            // Sort by key
krsort($user);                           // Sort by key descending

// Custom sorting
usort($data, function($a, $b) {
    return $a['age'] <=> $b['age'];      // Sort by age
});

// Natural order sorting
$files = ["img1.jpg", "img10.jpg", "img2.jpg"];
natsort($files);                         // ["img1.jpg", "img2.jpg", "img10.jpg"]

// Reversing
$reversed = array_reverse($fruits);

// Shuffling (random order)
shuffle($fruits);                        // Modifies original array

// Merging
$combined = array_merge($array1, $array2);
$combined = [...$array1, ...$array2];    // Spread operator (PHP 7.4+)

// Difference and intersection
$diff = array_diff($array1, $array2);    // In 1 but not in 2
$common = array_intersect($array1, $array2);

// Unique values
$unique = array_unique($array);

// Flip keys and values
$flipped = array_flip(["a" => 1, "b" => 2]);  // [1 => "a", 2 => "b"]

// Fill
$filled = array_fill(0, 5, "value");     // ["value", "value", "value", "value", "value"]

// Chunk
$chunks = array_chunk($largeArray, 10);  // Split into arrays of 10
?>
```

### Array Functions (Functional Programming)

**Definition:** PHP offers powerful functional programming functions for arrays: `array_map()` (applies a callback to each element), `array_filter()` (filters elements based on a callback), and `array_reduce()` (reduces the array to a single value). These promote cleaner, more declarative code compared to `foreach` loops for data transformation.

```php
<?php
$numbers = [1, 2, 3, 4, 5];
$users = [
    ["name" => "John", "age" => 30],
    ["name" => "Jane", "age" => 25],
    ["name" => "Bob", "age" => 35],
];

// array_map - transform each element
$doubled = array_map(fn($n) => $n * 2, $numbers);  // [2, 4, 6, 8, 10]

// With multiple arrays
$sums = array_map(fn($a, $b) => $a + $b, [1, 2, 3], [10, 20, 30]);  // [11, 22, 33]

// array_filter - keep elements that match condition
$evens = array_filter($numbers, fn($n) => $n % 2 === 0);  // [2, 4] (preserves keys)
$evens = array_values($evens);  // Re-index: [0 => 2, 1 => 4]

// array_reduce - reduce to single value
$sum = array_reduce($numbers, fn($carry, $n) => $carry + $n, 0);  // 15
$product = array_reduce($numbers, fn($c, $n) => $c * $n, 1);  // 120

// array_walk - apply function to each element (modifies in place)
array_walk($numbers, function(&$value, $key) {
    $value *= 2;
});

// array_column - extract single column
$names = array_column($users, "name");  // ["John", "Jane", "Bob"]

// With key
$userByName = array_column($users, null, "name");
// ["John" => [...], "Jane" => [...], "Bob" => [...]]

// array_combine - create array from keys and values
$keys = ["a", "b", "c"];
$values = [1, 2, 3];
$combined = array_combine($keys, $values);  // ["a" => 1, "b" => 2, "c" => 3]

// array_keys and array_values
$keys = array_keys($user);       // ["name", "email", "age"]
$values = array_values($user);   // ["John", "john@example.com", 25]

// Checking if all/any match
$allPositive = array_reduce($numbers, fn($c, $n) => $c && $n > 0, true);
$anyNegative = array_reduce($numbers, fn($c, $n) => $c || $n < 0, false);

// array_find (PHP 8.4+)
$firstAdult = array_find($users, fn($u) => $u['age'] >= 18);

// array_any / array_all (PHP 8.4+)
$allAdults = array_all($users, fn($u) => $u['age'] >= 18);
$anySenior = array_any($users, fn($u) => $u['age'] >= 65);
?>
```

### Array Destructuring

**Definition:** Array destructuring (available since PHP 7.1) allows unpacking array values into individual variables. It uses the `[]` syntax on the left side of an assignment (essentially the symmetrical definition of array creation). Indices can be skipped, and string keys can be destructured (`['id' => $id] = $user`).

```php
<?php
// List destructuring
$coords = [10, 20];
[$x, $y] = $coords;  // PHP 7.1+
list($x, $y) = $coords;  // Older syntax

// Associative destructuring
$user = ["name" => "John", "age" => 30, "city" => "NYC"];
["name" => $name, "age" => $age] = $user;  // Extract specific keys

// Nested destructuring
$matrix = [[1, 2], [3, 4]];
[[$a, $b], [$c, $d]] = $matrix;
// $a=1, $b=2, $c=3, $d=4

// Swapping variables
$a = 1;
$b = 2;
[$a, $b] = [$b, $a];  // Now $a=2, $b=1

// With foreach
$users = [
    ["name" => "John", "email" => "john@example.com"],
    ["name" => "Jane", "email" => "jane@example.com"],
];

foreach ($users as ["name" => $name, "email" => $email]) {
    echo "$name: $email\n";
}

// Spread operator in arrays
$arr1 = [1, 2, 3];
$arr2 = [4, 5, 6];
$combined = [...$arr1, ...$arr2];  // [1, 2, 3, 4, 5, 6]

// With associative arrays
$defaults = ["timeout" => 30, "retries" => 3];
$config = [...$defaults, "timeout" => 60];  // Override timeout
?>
```

---

## 8. Superglobals

### Definition
Superglobals are built-in variables that are always available in all scopes. They provide access to request data, server information, sessions, and more. Superglobals are accessible from any function, class, or file without needing to declare them as global.

### Superglobals Reference

| Superglobal | Type | Description |
|-------------|------|-------------|
| `$_GET` | HTTP Request | URL parameters (query string) |
| `$_POST` | HTTP Request | Form data sent via HTTP POST |
| `$_REQUEST` | HTTP Request | Merged `$_GET`, `$_POST`, and `$_COOKIE` |
| `$_FILES` | HTTP Request | File upload information |
| `$_SESSION` | Session | Server-side session variables |
| `$_COOKIE` | Session | Client-side cookie data |
| `$_ENV` | Environment | Environment variables (if populated) |
| `$_SERVER` | Server Info | Server and execution environment info |
| `$GLOBALS` | Global Scope | All global variables in script |


### $_GET

**Definition:** `$_GET` is a superglobal array that collects data sent via URL parameters (query string). It is visible in the URL (e.g., `page.php?id=5`) and should strictly be used for retrieving data (idempotent requests), never for sensitive data (passwords) or modifying server state.

```php
<?php
// URL: /page.php?name=John&age=25

// $_GET contains URL parameters
$name = $_GET['name'];    // "John"
$age = $_GET['age'];      // "25" (always a string)

// Check if parameter exists
if (isset($_GET['search'])) {
    $search = $_GET['search'];
}

// With null coalescing
$page = $_GET['page'] ?? 1;  // Default to 1 if not set

// Array parameters
// URL: /page.php?color[]=red&color[]=blue
$colors = $_GET['color'];  // ["red", "blue"]

// Always sanitize user input!
$name = htmlspecialchars($_GET['name'] ?? '', ENT_QUOTES, 'UTF-8');
?>
```

### $_POST

**Definition:** `$_POST` is a superglobal array that collects data sent via the HTTP POST method. Data is sent in the request body, not the URL, making it invisible to the user and suitable for sensitive data (passwords) and large payloads. Standard for submitting forms that modify server state.

```php
<?php
// $_POST contains HTTP POST data (form submissions)

// HTML form: <form method="POST" action="submit.php">
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $email = $_POST['email'] ?? '';
    $password = $_POST['password'] ?? '';
    
    // Always validate and sanitize!
    $email = filter_var($email, FILTER_SANITIZE_EMAIL);
    
    if (filter_var($email, FILTER_VALIDATE_EMAIL)) {
        // Valid email, process form
    }
}

// Check if form was submitted
if (!empty($_POST)) {
    // Form data received
}
?>
```

### $_REQUEST

**Definition:** `$_REQUEST` is a superglobal array that contains the contents of `$_GET`, `$_POST`, and `$_COOKIE` by default. While convenient, it is generally discouraged because it obscures the origin of the data and can lead to security vulnerabilities if not handled carefully. Prefer specific superglobals like `$_POST` or `$_GET`.

```php
<?php
// $_REQUEST contains $_GET, $_POST, and $_COOKIE combined
// Order determined by request_order/variables_order in php.ini

// Generally avoid - use $_GET or $_POST explicitly for clarity
$name = $_REQUEST['name'];  // Could be from GET or POST
?>
```

### $_SERVER

**Definition:** `$_SERVER` is a superglobal array containing information about headers, paths, and script locations provided by the web server. Key indices include `REQUEST_METHOD` (GET/POST), `SERVER_NAME` (hostname), `PHP_SELF` (current script), and `REMOTE_ADDR` (client IP). It bridges the gap between PHP and the underlying server environment.

```php
<?php
// $_SERVER contains server and execution environment information

// Common $_SERVER variables
$_SERVER['REQUEST_METHOD'];     // GET, POST, PUT, DELETE, etc.
$_SERVER['REQUEST_URI'];         // /path/to/page?query=string
$_SERVER['QUERY_STRING'];        // query=string (without ?)
$_SERVER['SCRIPT_NAME'];         // /path/to/script.php
$_SERVER['PHP_SELF'];            // /path/to/script.php
$_SERVER['HTTP_HOST'];           // www.example.com
$_SERVER['HTTP_USER_AGENT'];     // Mozilla/5.0...
$_SERVER['HTTP_REFERER'];        // Previous page URL (if available)
$_SERVER['REMOTE_ADDR'];         // Client IP address
$_SERVER['SERVER_NAME'];         // Server hostname
$_SERVER['SERVER_ADDR'];         // Server IP address
$_SERVER['SERVER_PORT'];         // 80, 443, etc.
$_SERVER['HTTPS'];               // "on" if using HTTPS
$_SERVER['DOCUMENT_ROOT'];       // /var/www/html

// Check if HTTPS
$isHttps = isset($_SERVER['HTTPS']) && $_SERVER['HTTPS'] === 'on';

// Get client IP (with proxy handling)
$ip = $_SERVER['HTTP_X_FORWARDED_FOR'] ?? $_SERVER['REMOTE_ADDR'];

// Current URL
$protocol = isset($_SERVER['HTTPS']) ? 'https' : 'http';
$currentUrl = $protocol . "://" . $_SERVER['HTTP_HOST'] . $_SERVER['REQUEST_URI'];

// Check request method
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // Handle POST request
}
?>
```

### $_SESSION

**Definition:** `$_SESSION` is a superglobal array used to store user information across multiple pages (e.g., login state, shopping cart). Unlike cookies, session data is stored on the server, with only a unique Session ID stored on the client (in a cookie). This makes it secure for sensitive state.

```php
<?php
// Must start session before using $_SESSION
session_start();

// Store data in session
$_SESSION['user_id'] = 123;
$_SESSION['username'] = 'john_doe';
$_SESSION['cart'] = ['item1', 'item2'];

// Access session data
echo $_SESSION['username'];  // "john_doe"

// Check if session variable exists
if (isset($_SESSION['user_id'])) {
    // User is logged in
}

// Remove session variable
unset($_SESSION['username']);

// Destroy entire session
session_destroy();
$_SESSION = [];  // Clear session array

// Regenerate session ID (security - prevent fixation)
session_regenerate_id(true);

// Flash messages pattern
if (!isset($_SESSION['flash'])) {
    $_SESSION['flash'] = [];
}
$_SESSION['flash']['success'] = 'Profile updated!';

// Display and clear
if (isset($_SESSION['flash']['success'])) {
    echo $_SESSION['flash']['success'];
    unset($_SESSION['flash']['success']);
}
?>
```

### $_COOKIE

**Definition:** `$_COOKIE` is a superglobal array containing data stored in cookies solely on the client's browser. Cookies are sent with every HTTP request. They are used for tracking, remembering preferences (like dark mode), or storing simple state that doesn't require server-side security.

```php
<?php
// $_COOKIE contains HTTP Cookies

// Read cookie
$username = $_COOKIE['username'] ?? 'Guest';

// Set cookie (must be done before any output!)
// setcookie(name, value, expire, path, domain, secure, httponly)
setcookie('username', 'john', time() + 3600, '/');  // Expires in 1 hour

// Delete cookie
setcookie('username', '', time() - 3600, '/');  // Set expiration in past

// Secure cookie (HTTPS only)
setcookie('token', $value, [
    'expires' => time() + 3600,
    'path' => '/',
    'secure' => true,      // HTTPS only
    'httponly' => true,    // Not accessible via JavaScript
    'samesite' => 'Strict' // CSRF protection
]);
?>
```

### $_FILES

**Definition:** `$_FILES` is a superglobal array containing information about files uploaded via HTTP POST. For each file, it provides the name, type, temp_name (location on server), error code, and size. The form must use `enctype="multipart/form-data"` for this array to be populated.

```php
<?php
// $_FILES contains uploaded file information

// HTML: <input type="file" name="avatar">

if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_FILES['avatar'])) {
    $file = $_FILES['avatar'];
    
    // File information
    $file['name'];        // Original filename (user-provided, not safe!)
    $file['tmp_name'];    // Temporary path on server
    $file['size'];        // Size in bytes
    $file['type'];        // MIME type (user-provided, not reliable!)
    $file['error'];       // Error code (0 = success)
    
    // Check for errors
    if ($file['error'] === UPLOAD_ERR_OK) {
        // Validate file
        $allowed = ['image/jpeg', 'image/png', 'image/gif'];
        $finfo = finfo_open(FILEINFO_MIME_TYPE);
        $mime = finfo_file($finfo, $file['tmp_name']);
        finfo_close($finfo);
        
        if (!in_array($mime, $allowed)) {
            die('Invalid file type');
        }
        
        // Check size (max 2MB)
        if ($file['size'] > 2 * 1024 * 1024) {
            die('File too large');
        }
        
        // Generate safe filename
        $extension = pathinfo($file['name'], PATHINFO_EXTENSION);
        $newName = uniqid() . '.' . $extension;
        $destination = 'uploads/' . $newName;
        
        // Move uploaded file
        if (move_uploaded_file($file['tmp_name'], $destination)) {
            echo 'File uploaded successfully!';
        }
    }
}

// Multiple file upload
// HTML: <input type="file" name="photos[]" multiple>
if (isset($_FILES['photos'])) {
    foreach ($_FILES['photos']['tmp_name'] as $index => $tmpName) {
        if ($_FILES['photos']['error'][$index] === UPLOAD_ERR_OK) {
            // Process each file
            move_uploaded_file($tmpName, 'uploads/' . $_FILES['photos']['name'][$index]);
        }
    }
}
?>
```

### $_ENV

**Definition:** `$_ENV` is a superglobal array containing environment variables. These are often set by the shell or server configuration. In modern PHP development (like Laravel), environment variables (stored in `.env` files) are the standard way to manage configuration secrets like API keys and database credentials.

```php
<?php
// $_ENV contains environment variables

// Common usage: configuration
db_host = $_ENV['DB_HOST'] ?? 'localhost';
$db_name = $_ENV['DB_NAME'] ?? 'myapp';

// Better: use getenv() for environment variables
$apiKey = getenv('API_KEY');

// With fallback
$debug = filter_var(getenv('DEBUG') ?: 'false', FILTER_VALIDATE_BOOLEAN);

// Loading from .env file (using library like vlucas/phpdotenv)
// require 'vendor/autoload.php';
// $dotenv = Dotenv\Dotenv::createImmutable(__DIR__);
// $dotenv->load();
// $dbHost = $_ENV['DB_HOST'];
?>
```

### $GLOBALS

**Definition:** `$GLOBALS` is a superglobal array that references all variables available in the global scope. It allows accessing global variables from within functions or methods without using the `global` keyword. While part of the language, relying on global state is widely considered an anti-pattern in modern PHP.

```php
<?php
// $GLOBALS contains all global variables

$globalVar = "I'm global";

function test() {
    // Access global variable
    echo $GLOBALS['globalVar'];
    
    // Equivalent to:
    global $globalVar;
    echo $globalVar;
}

// Can also set globals
function setGlobal($value) {
    $GLOBALS['globalVar'] = $value;
}
?>
```

---

## 9. Forms & Input Handling

### Definition
Forms are the primary way to collect user input. PHP handles form data securely through validation, sanitization, and proper escaping. Never trust user input - always validate on the server side regardless of client-side validation.

### Form Submission Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                FORM SUBMISSION PROCESS                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  BROWSER                      SERVER                            │
│  ────────                     ──────                            │
│                                                                 │
│  ┌─────────────┐                                              │
│  │ HTML Form   │                                              │
│  │             │                                              │
│  │ <form       │   1. SUBMIT                                  │
│  │   method=   │ ──────────────> ┌─────────────────────┐     │
│  │   "POST">   │   HTTP POST     │                     │     │
│  │  <input     │   data to       │   PHP PROCESSING    │     │
│  │   name="x"> │   process.php   │                     │     │
│  │ </form>     │                 │  2. RECEIVE         │     │
│  └─────────────┘                 │     $_POST data     │     │
│                                  │                     │     │
│                                  │  3. VALIDATE        │     │
│                                  │     • Required?     │     │
│                                  │     • Format?       │     │
│                                  │     • Length?       │     │
│                                  │                     │     │
│                                  │  4. SANITIZE        │     │
│                                  │     htmlspecialchars│     │
│                                  │     filter_var()    │     │
│                                  │                     │     │
│                                  │  5. PROCESS         │     │
│                                  │     Save to DB      │     │
│                                  │     Send email      │     │
│                                  │                     │     │
│  ┌─────────────┐                 │  6. RESPONSE        │     │
│  │  Success/   │ <────────────── │     Redirect/       │     │
│  │  Error Page │   HTTP Response │     Show result     │     │
│  └─────────────┘                 └─────────────────────┘     │
│                                                                 │
│  ⚠️  SECURITY CHECKPOINTS:                                      │
│      □ CSRF token validation                                    │
│      □ Input validation (never trust client-side only)          │
│      □ Output escaping (prevent XSS)                            │
│      □ SQL injection prevention (prepared statements)           │
└─────────────────────────────────────────────────────────────────┘
```

### Processing Form Data

**Definition:** Processing form data involves receiving input (typically `$_POST`), verifying the request method, validating the data (checking constraints), sanitizing it (cleaning/escaping), and then performing an action (saving to DB, sending email). It is the core interaction pattern in dynamic web applications.

```php
<?php
// HTML form:
/*
<form method="POST" action="process.php">
    <input type="text" name="username" required>
    <input type="email" name="email" required>
    <textarea name="message"></textarea>
    <button type="submit">Submit</button>
</form>
*/

// process.php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // Retrieve form data
    $username = $_POST['username'] ?? '';
    $email = $_POST['email'] ?? '';
    $message = $_POST['message'] ?? '';
    
    // Initialize errors array
    $errors = [];
    
    // Validation
    if (empty($username)) {
        $errors[] = "Username is required";
    } elseif (strlen($username) < 3) {
        $errors[] = "Username must be at least 3 characters";
    }
    
    if (empty($email)) {
        $errors[] = "Email is required";
    } elseif (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
        $errors[] = "Invalid email format";
    }
    
    // If no errors, process data
    if (empty($errors)) {
        // Sanitize for database storage
        $username = htmlspecialchars($username, ENT_QUOTES, 'UTF-8');
        $email = filter_var($email, FILTER_SANITIZE_EMAIL);
        $message = htmlspecialchars($message, ENT_QUOTES, 'UTF-8');
        
        // Save to database, send email, etc.
        echo "Form submitted successfully!";
    } else {
        // Display errors
        foreach ($errors as $error) {
            echo "<p class='error'>$error</p>";
        }
    }
}
?>
```

### Input Sanitization & Validation

**Definition:** **Validation** ensures data matches expected formats (e.g., strict email format, required fields). **Sanitization** cleans data to prevent security issues (e.g., removing HTML tags to prevent XSS). PHP provides `filter_var()` with specific filters (`FILTER_VALIDATE_EMAIL`, `FILTER_SANITIZE_STRING`) to handle both robustly.

```php
<?php
// filter_input - get and filter in one step
$email = filter_input(INPUT_POST, 'email', FILTER_VALIDATE_EMAIL);
$age = filter_input(INPUT_GET, 'age', FILTER_VALIDATE_INT);
$page = filter_input(INPUT_GET, 'page', FILTER_VALIDATE_INT) ?: 1;

// filter_var - validate/sanitize variables
$email = "user@example.com";
if (filter_var($email, FILTER_VALIDATE_EMAIL)) {
    echo "Valid email";
}

// Common filters
FILTER_VALIDATE_BOOLEAN;      // true/false
FILTER_VALIDATE_EMAIL;        // Email format
FILTER_VALIDATE_FLOAT;        // Float number
FILTER_VALIDATE_INT;          // Integer
FILTER_VALIDATE_IP;           // IP address
FILTER_VALIDATE_MAC;          // MAC address
FILTER_VALIDATE_REGEXP;       // Regular expression
FILTER_VALIDATE_URL;          // URL format

// Sanitization filters
FILTER_SANITIZE_EMAIL;        // Remove invalid email chars
FILTER_SANITIZE_ENCODED;      // URL encode
FILTER_SANITIZE_NUMBER_FLOAT; // Remove non-float chars
FILTER_SANITIZE_NUMBER_INT;   // Remove non-int chars
FILTER_SANITIZE_SPECIAL_CHARS;// HTML escape
FILTER_SANITIZE_STRING;       // Strip tags (deprecated, use htmlspecialchars)
FILTER_SANITIZE_URL;          // Remove invalid URL chars

// Custom filter with options
$options = [
    'options' => [
        'min_range' => 18,
        'max_range' => 120
    ]
];
$age = filter_var($input, FILTER_VALIDATE_INT, $options);

// Validate array of inputs
$filters = [
    'name' => FILTER_SANITIZE_SPECIAL_CHARS,
    'age' => [
        'filter' => FILTER_VALIDATE_INT,
        'options' => ['min_range' => 0, 'max_range' => 150]
    ],
    'email' => FILTER_VALIDATE_EMAIL,
    'website' => FILTER_VALIDATE_URL
];

$inputs = filter_input_array(INPUT_POST, $filters);

// Output escaping - ALWAYS use when displaying user input
$userInput = "<script>alert('xss')</script>";
echo htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');
// Output: &lt;script&gt;alert(&#039;xss&#039;)&lt;/script&gt;

// Context-aware escaping
// HTML content
htmlspecialchars($text, ENT_QUOTES, 'UTF-8');

// HTML attribute
htmlspecialchars($attr, ENT_QUOTES, 'UTF-8');

// JavaScript
json_encode($data, JSON_HEX_TAG | JSON_HEX_APOS | JSON_HEX_QUOT | JSON_HEX_AMP);

// URL
urlencode($string);   // For query parameters
rawurlencode($string); // For path segments

// CSS (no built-in function, whitelist allowed characters)
$safeCss = preg_replace('/[^a-zA-Z0-9\-#.,\s]/', '', $css);
?>
```

### CSRF Protection

**Definition:** CSRF (Cross-Site Request Forgery) protection prevents attackers from forcing authenticated users to submit unauthorized commands. It typically uses a unique, hidden token field in every form (`$_SESSION['csrf_token']`). The server verifies that the submitted token matches the stored session token before processing any state-changing request.

```php
<?php
// Generate CSRF token
session_start();

function generateCsrfToken() {
    if (!isset($_SESSION['csrf_token'])) {
        $_SESSION['csrf_token'] = bin2hex(random_bytes(32));
    }
    return $_SESSION['csrf_token'];
}

function validateCsrfToken($token) {
    return isset($_SESSION['csrf_token']) && 
           hash_equals($_SESSION['csrf_token'], $token);
}

// In form:
/*
<form method="POST" action="process.php">
    <input type="hidden" name="csrf_token" value="<?= htmlspecialchars(generateCsrfToken()) ?>">
    <!-- form fields -->
</form>
*/

// Validate on submission:
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $token = $_POST['csrf_token'] ?? '';
    
    if (!validateCsrfToken($token)) {
        die('Invalid CSRF token');
    }
    
    // Process form...
}
?>
```

### File Uploads

**Definition:** PHP handles file uploads via the `$_FILES` array. The process involves checking for upload errors, validating file type (MIME type) and size, generating a secure filename (to prevent overwrites/execution), and moving the file from `tmp_name` to its final destination using `move_uploaded_file()`.

```
┌─────────────────────────────────────────────────────────────────┐
│                  FILE UPLOAD PROCESS                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  BROWSER                              SERVER                    │
│  ────────                             ──────                    │
│                                                                 │
│  ┌─────────────────────┐                                        │
│  │ 1. USER SELECTS     │                                        │
│  │    FILE             │                                        │
│  │                     │                                        │
│  │ <input type="file"> │                                        │
│  └──────────┬──────────┘                                        │
│             │                                                   │
│             ▼                                                   │
│  ┌─────────────────────┐                                        │
│  │ 2. FORM SUBMITTED   │  HTTP POST (multipart/form-data)       │
│  │                     │ ────────────────────────────────>      │
│  │ enctype="multipart/ │    ┌─────────────────────────┐        │
│  │ form-data"          │    │ PHP RECEIVES $_FILES    │        │
│  └─────────────────────┘    │                         │        │
│                             │ $_FILES['avatar']       │        │
│                             │ ├── name                │        │
│                             │ ├── tmp_name            │        │
│                             │ ├── size                │        │
│                             │ ├── type (untrusted!)   │        │
│                             │ └── error               │        │
│                             │                         │        │
│                             └───────────┬─────────────┘        │
│                                         │                       │
│  ┌──────────────────────────────────────┴──────────────────┐   │
│  │              VALIDATION & SECURITY CHECKS                │   │
│  │                                                          │   │
│  │  3. CHECK ERROR      if ($file['error'] !== UPLOAD_ERR_OK)│   │
│  │                      │                                    │   │
│  │                      ▼                                    │   │
│  │  4. VERIFY MIME      finfo_file(FILEINFO_MIME_TYPE)       │   │
│  │     (Don't trust     │                                    │   │
│  │      $file['type']!) ▼                                    │   │
│  │  5. CHECK SIZE       if ($file['size'] > $maxSize)        │   │
│  │                      │                                    │   │
│  │                      ▼                                    │   │
│  │  6. SAFE FILENAME    bin2hex(random_bytes(16))            │   │
│  │     (Never use       NOT: $file['name'] (dangerous!)      │   │
│  │      original name)                                       │   │
│  │                      ▼                                    │   │
│  │  7. MOVE FILE        move_uploaded_file()                 │   │
│  │     (Use this function ONLY - security check)            │   │
│  │                      │                                    │   │
│  │                      ▼                                    │   │
│  │  8. SAVE PATH        Store in DB                          │   │
│  │                      to 'uploads/'                        │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ⚠️  CRITICAL: Always validate MIME type with finfo_file()      │
│      Never trust $_FILES['xxx']['type'] - it's client-provided  │
└─────────────────────────────────────────────────────────────────┘
```

```php
<?php
// Secure file upload handling
class FileUploader {
    private $allowedTypes = ['image/jpeg', 'image/png', 'image/gif'];
    private $maxSize = 2 * 1024 * 1024;  // 2MB
    private $uploadDir = 'uploads/';
    
    public function upload($file) {
        // Check for upload errors
        if ($file['error'] !== UPLOAD_ERR_OK) {
            throw new Exception('Upload failed with error code: ' . $file['error']);
        }
        
        // Verify file type (don't trust $file['type'])
        $finfo = finfo_open(FILEINFO_MIME_TYPE);
        $mimeType = finfo_file($finfo, $file['tmp_name']);
        finfo_close($finfo);
        
        if (!in_array($mimeType, $this->allowedTypes)) {
            throw new Exception('Invalid file type');
        }
        
        // Check file size
        if ($file['size'] > $this->maxSize) {
            throw new Exception('File too large');
        }
        
        // Generate safe filename (don't use original name!)
        $extension = pathinfo($file['name'], PATHINFO_EXTENSION);
        $filename = bin2hex(random_bytes(16)) . '.' . $extension;
        $destination = $this->uploadDir . $filename;
        
        // Ensure upload directory exists and is secure
        if (!is_dir($this->uploadDir)) {
            mkdir($this->uploadDir, 0755, true);
        }
        
        // Move file
        if (!move_uploaded_file($file['tmp_name'], $destination)) {
            throw new Exception('Failed to move uploaded file');
        }
        
        return $filename;
    }
}

// Usage
try {
    $uploader = new FileUploader();
    $filename = $uploader->upload($_FILES['avatar']);
    echo "File uploaded: $filename";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
?>
```

---

## 10. Working with Files

### Definition
PHP provides functions to read, write, and manipulate files on the server filesystem.

### Reading Files

**Definition:** PHP offers multiple ways to read files. `file_get_contents()` reads an entire file into a string (simplest). `readfile()` outputs a file directly to the buffer (fastest for downloads). `fopen()`/`fread()`/`fgets()` offer granular control (stream-based) for reading large files line-by-line without loading everything into memory.

```php
<?php
// file_get_contents - read entire file into string
$content = file_get_contents('data.txt');

// Read from URL (if allow_url_fopen is enabled)
$html = file_get_contents('https://api.example.com/data');

// Read with offset and limit
$partial = file_get_contents('large.txt', false, null, 0, 1000);

// file - read into array (one element per line)
$lines = file('data.txt');                    // Include newlines
$lines = file('data.txt', FILE_IGNORE_NEW_LINES);  // Exclude newlines
$lines = file('data.txt', FILE_SKIP_EMPTY_LINES);  // Skip empty lines

// fread with fopen (for large files)
$handle = fopen('large.txt', 'r');
if ($handle) {
    while (!feof($handle)) {
        $line = fgets($handle);  // Read line by line
        // Process line...
    }
    fclose($handle);
}

// Read CSV
$handle = fopen('data.csv', 'r');
while (($data = fgetcsv($handle, 1000, ',')) !== false) {
    // $data is array of CSV fields
    list($name, $email, $phone) = $data;
}
fclose($handle);

// Read specific bytes
$handle = fopen('binary.dat', 'rb');
$bytes = fread($handle, 1024);  // Read 1024 bytes
fclose($handle);

// Check if file exists and is readable
if (file_exists('data.txt') && is_readable('data.txt')) {
    $content = file_get_contents('data.txt');
}

// Get file info
echo filesize('data.txt');           // Size in bytes
echo filetype('data.txt');           // "file", "dir", etc.
echo filemtime('data.txt');          // Last modification time (timestamp)
echo filectime('data.txt');          // Creation time
echo mime_content_type('image.jpg'); // MIME type

// Path info
$info = pathinfo('/path/to/file.txt');
// $info['dirname'] = '/path/to'
// $info['basename'] = 'file.txt'
// $info['extension'] = 'txt'
// $info['filename'] = 'file'
?>
```

### Writing Files

**Definition:** Writing to files is handled primarily by `file_put_contents()` (simple, one-liner) or `fopen()`/`fwrite()` (stream-based). You can overwrite existing content or append to it (`FILE_APPEND` flag). Always ensure the server process has simple write permissions on the target directory.

```php
<?php
// file_put_contents - write string to file (simple)
file_put_contents('output.txt', 'Hello, World!');

// Append to file
file_put_contents('log.txt', "New entry\n", FILE_APPEND);

// Append with lock (prevents concurrent writes)
file_put_contents('log.txt', "New entry\n", FILE_APPEND | LOCK_EX);

// fwrite with fopen (more control)
$handle = fopen('output.txt', 'w');  // 'w' = write (truncate)
if ($handle) {
    fwrite($handle, "Line 1\n");
    fwrite($handle, "Line 2\n");
    fclose($handle);
}

// File modes:
// 'r'  - Read only, pointer at beginning
// 'r+' - Read/write, pointer at beginning
// 'w'  - Write only, truncate/create, pointer at beginning
// 'w+' - Read/write, truncate/create, pointer at beginning
// 'a'  - Write only, create if needed, pointer at end
// 'a+' - Read/write, create if needed, pointer at end
// 'x'  - Write only, create only (fail if exists)
// 'x+' - Read/write, create only
// 'b'  - Binary mode (append to any mode, e.g., 'rb')

// Write CSV
$handle = fopen('output.csv', 'w');
$data = [
    ['Name', 'Email', 'Phone'],
    ['John', 'john@example.com', '555-1234'],
    ['Jane', 'jane@example.com', '555-5678']
];

foreach ($data as $row) {
    fputcsv($handle, $row);
}
fclose($handle);

// Atomic write (write to temp, then rename)
function atomicWrite($filename, $content) {
    $temp = tempnam(dirname($filename), 'tmp');
    if (file_put_contents($temp, $content) === strlen($content)) {
        return rename($temp, $filename);
    }
    unlink($temp);
    return false;
}
?>
```

### File Operations

**Definition:** Common file system operations include checking existence (`file_exists`), checking type (`is_file`, `is_dir`), copying (`copy`), renaming/moving (`rename`), and deleting (`unlink`). PHP's filesystem functions are blocking (synchronous), so huge operations should be handled carefully.

```php
<?php
// Copy file
copy('source.txt', 'destination.txt');

// Rename/Move
rename('oldname.txt', 'newname.txt');
rename('/path/old.txt', '/other/path/new.txt');  // Move

// Delete
unlink('file.txt');

// Check existence
file_exists('file.txt');      // File or directory
is_file('file.txt');          // Is a file
is_dir('directory');          // Is a directory
is_readable('file.txt');      // Can be read
is_writable('file.txt');      // Can be written
is_executable('script.sh');   // Can be executed

// Directory operations
mkdir('new_directory');                    // Create directory
mkdir('path/to/nested/dir', 0755, true);   // Recursive create
rmdir('empty_directory');                  // Remove empty directory

// Scan directory
$files = scandir('.');                     // All files and dirs
$files = array_diff(scandir('.'), ['.', '..']);  // Exclude . and ..

// Directory iterator (better)
$iterator = new DirectoryIterator('.');
foreach ($iterator as $file) {
    if ($file->isFile()) {
        echo $file->getFilename() . "\n";
    }
}

// Recursive directory iterator
$iterator = new RecursiveIteratorIterator(
    new RecursiveDirectoryIterator('.')
);
foreach ($iterator as $file) {
    if ($file->isFile()) {
        echo $file->getPathname() . "\n";
    }
}

// Glob patterns
$phpFiles = glob('*.php');                 // All PHP files
$allFiles = glob('*');                     // All files
$images = glob('*.{jpg,png,gif}', GLOB_BRACE);  // Multiple extensions

// Temp files
$tempFile = tempnam(sys_get_temp_dir(), 'prefix');
$tempHandle = tmpfile();  // Creates and opens temp file, deleted on close
?>
```

---

## 11. Sessions & Cookies

### Definition
Sessions store data on the server for individual users. Cookies store small amounts of data on the client's browser. Sessions use a session ID stored in a cookie to link the browser to server-side data, providing a way to maintain state across multiple page requests.

### Session Lifecycle

```
┌─────────────────────────────────────────────────────────────────┐
│                   SESSION LIFECYCLE                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  FIRST VISIT                    SUBSEQUENT VISITS               │
│  ───────────                    ───────────────                 │
│                                                                 │
│  ┌──────────┐                   ┌──────────┐                    │
│  │ Browser  │                   │ Browser  │                    │
│  │ (No PHP  │                   │ (Has PHP │                    │
│  │ session  │                   │SESSID    │                    │
│  │ cookie)  │                   │ cookie)  │                    │
│  └────┬─────┘                   └────┬─────┘                    │
│       │                              │                          │
│       │ Request                      │ Request + Cookie         │
│       ▼                              ▼                          │
│  ┌────────────────────┐         ┌────────────────────┐         │
│  │   SERVER           │         │   SERVER           │         │
│  │                    │         │                    │         │
│  │ session_start()    │         │ session_start()    │         │
│  │                    │         │                    │         │
│  │ 1. Generate        │         │ 1. Read session ID │         │
│  │    session ID      │         │    from cookie     │         │
│  │                    │         │                    │         │
│  │ 2. Create          │         │ 2. Load session    │         │
│  │    $_SESSION[]     │         │    data from       │         │
│  │    array           │         │    storage         │         │
│  │                    │         │                    │         │
│  │ 3. Set cookie:     │         │ 3. $_SESSION now   │         │
│  │    PHPSESSID=abc   │         │    contains user's │         │
│  │                    │         │    data            │         │
│  │ 4. Store session   │         │ 4. Update data:    │         │
│  │    data on server  │         │    $_SESSION['x']  │         │
│  │                    │         │    = 'y'           │         │
│  │                    │         │                    │         │
│  │ 5. Save session    │         │ 5. Save updated    │         │
│  │    data at end     │         │    session data    │         │
│  │    of request      │         │    at end          │         │
│  └──────────┬─────────┘         └──────────┬─────────┘         │
│             │                              │                    │
│             │ Set Cookie                   │ Update Session     │
│             ▼                              ▼                    │
│       ┌──────────┐                   ┌──────────┐              │
│       │ Browser  │                   │ Browser  │              │
│       │ (Now has │                   │ (Session │              │
│       │ session  │                   │ continues│              │
│       │ cookie)  │                   │ )        │              │
│       └──────────┘                   └──────────┘              │
│                                                                 │
│  SESSION STORAGE OPTIONS:                                       │
│  • Files (default) - /var/lib/php/sessions/                     │
│  • Database - Custom session handler                            │
│  • Redis/Memcached - High-performance options                   │
│                                                                 │
│  SESSION SECURITY:                                              │
│  • Regenerate ID on login (prevent fixation)                    │
│  • Use httpOnly, secure, SameSite cookie flags                  │
│  • Set reasonable timeout (gc_maxlifetime)                      │
└─────────────────────────────────────────────────────────────────┘
```

### Sessions

**Definition:** Sessions allow you to store user information on the server for later use across multiple pages (e.g., login status, shopping cart). Unlike cookies, session data is stored on the server, offering better security for sensitive data. PHP handles session management automatically via `session_start()` and the `$_SESSION` superglobal.

```php
<?php
// Start session (must be before any output!)
session_start();

// Store session data
$_SESSION['user_id'] = 123;
$_SESSION['username'] = 'john_doe';
$_SESSION['login_time'] = time();
$_SESSION['cart'] = [];

// Access session data
echo $_SESSION['username'] ?? 'Guest';

// Check if logged in
function isLoggedIn() {
    return isset($_SESSION['user_id']);
}

// Update session
$_SESSION['last_activity'] = time();

// Remove specific session variable
unset($_SESSION['cart']);

// Destroy entire session
function logout() {
    // Clear session data
    $_SESSION = [];
    
    // Destroy session cookie
    if (isset($_COOKIE[session_name()])) {
        setcookie(session_name(), '', [
            'expires' => time() - 3600,
            'path' => '/',
            'secure' => true,
            'httponly' => true,
            'samesite' => 'Strict'
        ]);
    }
    
    // Destroy session
    session_destroy();
}

// Session security
// Regenerate ID after login (prevent fixation)
function login($userId) {
    session_regenerate_id(true);  // Delete old session
    $_SESSION['user_id'] = $userId;
}

// Session timeout
function checkSessionTimeout($timeout = 1800) {  // 30 minutes
    if (isset($_SESSION['last_activity']) && 
        (time() - $_SESSION['last_activity'] > $timeout)) {
        logout();
        return false;
    }
    $_SESSION['last_activity'] = time();
    return true;
}

// Custom session handler (database-backed sessions)
// session_set_save_handler($handler, true);

// Session configuration
ini_set('session.cookie_httponly', 1);      // Not accessible via JS
ini_set('session.cookie_secure', 1);         // HTTPS only
ini_set('session.cookie_samesite', 'Strict'); // CSRF protection
ini_set('session.use_strict_mode', 1);       // Reject uninitialized IDs
ini_set('session.gc_maxlifetime', 1800);     // 30 minute timeout
?>
```

### Cookies

```php
<?php
// Set cookie (must be before any output!)
// setcookie(name, value, expires, path, domain, secure, httponly, samesite)

// Basic cookie
setcookie('username', 'john', time() + 3600);  // Expires in 1 hour

// Secure cookie
setcookie('remember_me', $token, [
    'expires' => time() + 86400 * 30,  // 30 days
    'path' => '/',
    'domain' => '.example.com',         // Available on all subdomains
    'secure' => true,                   // HTTPS only
    'httponly' => true,                 // Not accessible via JavaScript
    'samesite' => 'Strict'              // Strict, Lax, or None
]);

// Read cookie
$username = $_COOKIE['username'] ?? 'Guest';

// Update cookie (set again with new value)
setcookie('username', 'jane', time() + 3600);

// Delete cookie (set expiration in past)
setcookie('username', '', [
    'expires' => time() - 3600,
    'path' => '/'
]);
unset($_COOKIE['username']);  // Remove from current request

// Cookie best practices
// 1. Don't store sensitive data in cookies
// 2. Use httponly to prevent XSS
// 3. Use secure flag for HTTPS
// 4. Use samesite for CSRF protection
// 5. Keep expiration reasonable
// 6. Validate cookie data (don't trust it!)

// Remember me functionality (secure)
function setRememberMe($userId) {
    $selector = bin2hex(random_bytes(12));
    $validator = bin2hex(random_bytes(32));
    
    // Store hashed validator in database
    $hashedValidator = hash('sha256', $validator);
    saveRememberMeToken($userId, $selector, $hashedValidator);
    
    // Set cookie with selector:validator
    $cookieValue = $selector . ':' . $validator;
    setcookie('remember', $cookieValue, [
        'expires' => time() + 86400 * 30,
        'path' => '/',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'Strict'
    ]);
}
?>
```

---

## 12. Error Handling

### Definition
PHP has multiple error types and supports exception handling for robust error management. Understanding error levels, custom error handlers, and exception handling is crucial for building reliable applications that fail gracefully.

### Error Handling Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                  ERROR HANDLING FLOW                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ERROR OCCURS                                                   │
│       │                                                         │
│       ▼                                                         │
│  ┌──────────────────────────────────────────────────────┐      │
│  │              ERROR TYPES                             │      │
│  │                                                      │      │
│  │  ┌────────────┐  ┌────────────┐  ┌────────────┐     │      │
│  │  │  FATAL     │  │  WARNING   │  │   NOTICE   │     │      │
│  │  │  E_ERROR   │  │ E_WARNING  │  │  E_NOTICE  │     │      │
│  │  │            │  │            │  │            │     │      │
│  │  │ Stops      │  │ Continues  │  │ Continues  │     │      │
│  │  │ execution  │  │ execution  │  │ execution  │     │      │
│  │  └─────┬──────┘  └─────┬──────┘  └─────┬──────┘     │      │
│  │        │               │               │            │      │
│  │        └───────────────┼───────────────┘            │      │
│  │                        ▼                            │      │
│  │              ┌──────────────────┐                   │      │
│  │              │ CUSTOM HANDLER?  │                   │      │
│  │              │ set_error_handler│                   │      │
│  │              └────────┬─────────┘                   │      │
│  └───────────────────────┼─────────────────────────────┘      │
│                          │                                     │
│           ┌──────────────┼──────────────┐                     │
│           │              │              │                     │
│           ▼              ▼              ▼                     │
│    ┌────────────┐ ┌────────────┐ ┌────────────┐              │
│    │   YES      │ │    NO      │ │ EXCEPTION  │              │
│    │            │ │            │ │ THROWN     │              │
│    │ Call       │ │ Default    │ │            │              │
│    │ custom     │ │ PHP        │ │ try {      │              │
│    │ handler    │ │ handler    │ │   throw    │              │
│    └─────┬──────┘ └─────┬──────┘ │ } catch()  │              │
│          │              │        └─────┬──────┘              │
│          ▼              ▼              │                       │
│  ┌───────────────────────────────────┼──────────┐            │
│  │         ERROR HANDLING STRATEGY   │          │            │
│  │                                   ▼          │            │
│  │   ┌─────────────────────────────────────┐   │            │
│  │   │  try {                              │   │            │
│  │   │      riskyOperation();              │   │            │
│  │   │  } catch (SpecificException $e) {   │   │            │
│  │   │      // Handle specific error       │   │            │
│  │   │  } catch (Exception $e) {           │   │            │
│  │   │      // Generic error handling      │   │            │
│  │   │  } finally {                        │   │            │
│  │   │      // Always execute (cleanup)    │   │            │
│  │   │  }                                  │   │            │
│  │   └─────────────────────────────────────┘   │            │
│  │                                              │            │
│  │   PRODUCTION vs DEVELOPMENT:                 │            │
│  │   • Dev: display_errors = On, show details   │            │
│  │   • Prod: display_errors = Off, log to file  │            │
│  └──────────────────────────────────────────────┘            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Error Types

**Definition:** PHP errors are categorized by severity. **Fatal Errors** (E_ERROR) stop script execution immediately. **Parse Errors** (E_PARSE) occur due to syntax mistakes. **Warnings** (E_WARNING) indicate non-fatal problems (execution continues). **Notices** (E_NOTICE) suggest potential bugs (like undefined variables) but don't halt execution. PHP 8 upgraded many warnings/notices to Fatal Errors or Exceptions.

```php
<?php
// PHP Error Levels:
// E_ERROR       - Fatal run-time errors (cannot recover)
// E_WARNING     - Run-time warnings (non-fatal)
// E_NOTICE      - Run-time notices (possible bugs)
// E_PARSE       - Compile-time parse errors
// E_DEPRECATED  - Deprecation warnings
// E_STRICT      - Strict coding suggestions
// E_ALL         - All errors and warnings

// Trigger custom error
trigger_error("Custom warning", E_USER_WARNING);
trigger_error("Custom notice", E_USER_NOTICE);
trigger_error("Fatal error", E_USER_ERROR);  // Terminates script

// Error reporting configuration
error_reporting(E_ALL);                      // Report all errors
error_reporting(E_ALL & ~E_NOTICE);          // All except notices
error_reporting(0);                          // Report no errors (production)
ini_set('display_errors', 1);                // Display errors
ini_set('log_errors', 1);                    // Log errors
ini_set('error_log', '/path/to/errors.log'); // Error log file

// Custom error handler
function customErrorHandler($errno, $errstr, $errfile, $errline) {
    $message = date('[Y-m-d H:i:s]') . " Error [$errno]: $errstr in $errfile on line $errline\n";
    
    // Log to file
    error_log($message, 3, '/var/log/php_errors.log');
    
    // Display user-friendly message (don't expose details!)
    if (ini_get('display_errors')) {
        echo "An error occurred. Please try again later.";
    }
    
    return true;  // Don't execute PHP's internal handler
}

set_error_handler('customErrorHandler');

// Restore default handler
restore_error_handler();
?>
```

### Exception Handling

**Definition:** Exceptions are an object-oriented way to handle errors gracefully. When an error occurs, an exception is "thrown". Code execution stops and jumps to the nearest "catch" block. If uncaught, it causes a Fatal Error. The `try...catch...finally` block allows you to attempt risky code and handle failures without crashing the application.

```php
<?php
// Basic try-catch
try {
    $result = divide(10, 0);
} catch (DivisionByZeroError $e) {
    echo "Cannot divide by zero";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}

// Multiple catch blocks
try {
    $data = fetchData();
    $result = process($data);
} catch (DatabaseException $e) {
    logError("Database error: " . $e->getMessage());
    echo "Database error occurred";
} catch (ValidationException $e) {
    echo "Invalid data: " . $e->getMessage();
} catch (Throwable $e) {  // Catches all errors and exceptions (PHP 7+)
    logError("Unexpected error: " . $e->getMessage());
    echo "An unexpected error occurred";
}

// Try-catch-finally
try {
    $file = fopen('data.txt', 'r');
    $content = fread($file, filesize('data.txt'));
    // Process content...
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
} finally {
    // Always executes (cleanup)
    if (isset($file) && is_resource($file)) {
        fclose($file);
    }
}

// Throwing exceptions
function divide($a, $b) {
    if ($b === 0) {
        throw new Exception("Division by zero");
    }
    return $a / $b;
}

// With typed properties
function connectToDatabase(array $config): PDO {
    if (!isset($config['host'], $config['dbname'], $config['user'])) {
        throw new InvalidArgumentException("Missing required config");
    }
    
    try {
        $pdo = new PDO(
            "mysql:host={$config['host']};dbname={$config['dbname']}",
            $config['user'],
            $config['password'] ?? ''
        );
        return $pdo;
    } catch (PDOException $e) {
        throw new DatabaseException("Connection failed", 0, $e);
    }
}

// Rethrowing exceptions
try {
    riskyOperation();
} catch (SpecificException $e) {
    // Handle specific case
    handleSpecificError($e);
} catch (Exception $e) {
    // Add context and rethrow
    throw new ApplicationException("Operation failed in module X", 0, $e);
}
?>
```

### Custom Exceptions

**Definition:** You can define your own exception classes by extending the built-in `Exception` class. This allows you to create specific error types for your application (e.g., `UserNotFoundException`, `DatabaseConnectionException`) and handle them differently in your catch blocks, improving code clarity and error management granularity.

```php
<?php
// Custom exception classes
class ValidationException extends Exception {
    private $errors;
    
    public function __construct(array $errors, $message = "Validation failed") {
        parent::__construct($message);
        $this->errors = $errors;
    }
    
    public function getErrors(): array {
        return $this->errors;
    }
}

class DatabaseException extends Exception {
    // Can add database-specific methods
    public function getSqlState(): ?string {
        // Implementation
        return null;
    }
}

class NotFoundException extends Exception {
    public function __construct(string $resource, $code = 404) {
        parent::__construct("$resource not found", $code);
    }
}

// Using custom exceptions
function validateUser(array $data): void {
    $errors = [];
    
    if (empty($data['email'])) {
        $errors['email'] = 'Email is required';
    } elseif (!filter_var($data['email'], FILTER_VALIDATE_EMAIL)) {
        $errors['email'] = 'Invalid email format';
    }
    
    if (empty($data['password']) || strlen($data['password']) < 8) {
        $errors['password'] = 'Password must be at least 8 characters';
    }
    
    if (!empty($errors)) {
        throw new ValidationException($errors);
    }
}

// Catch and handle
try {
    validateUser($_POST);
} catch (ValidationException $e) {
    // Display form errors
    foreach ($e->getErrors() as $field => $error) {
        echo "<p class='error'>$field: $error</p>";
    }
}
?>
```

---

## 13. Working with Databases (PDO)

### Definition
PDO (PHP Data Objects) provides a consistent interface for accessing databases in PHP. It supports prepared statements for security. PDO offers database abstraction, meaning you can switch between different database systems (MySQL, PostgreSQL, SQLite, etc.) with minimal code changes.

### PDO Prepared Statement Flow

```
┌─────────────────────────────────────────────────────────────────┐
│              PDO PREPARED STATEMENT EXECUTION                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  WITHOUT PREPARED STATEMENTS (DANGEROUS!)                       │
│  ───────────────────────────────────────                        │
│                                                                 │
│  $query = "SELECT * FROM users WHERE id = $userId";             │
│                                               │                 │
│                                               ▼                 │
│  If $userId = "1 OR 1=1" → SQL INJECTION!                       │
│  Returns ALL users instead of just user 1                       │
│                                                                 │
│  ═══════════════════════════════════════════════════════════    │
│                                                                 │
│  WITH PREPARED STATEMENTS (SECURE)                              │
│  ─────────────────────────────────                              │
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐      │
│  │ 1. PREPARE (One time)                                │      │
│  │                                                      │      │
│  │    $stmt = $pdo->prepare(                           │      │
│  │        "SELECT * FROM users WHERE id = :id"         │      │
│  │    );                                                │      │
│  │                                                      │      │
│  │    ↓                                                 │      │
│  │    SQL template sent to database                     │      │
│  │    Database compiles and optimizes                   │      │
│  │    Execution plan created                            │      │
│  └──────────────────────────────────────────────────────┘      │
│                           │                                     │
│                           ▼                                     │
│  ┌──────────────────────────────────────────────────────┐      │
│  │ 2. EXECUTE (Multiple times with different data)      │      │
│  │                                                      │      │
│  │    $stmt->execute([':id' => 1]);  ← User ID         │      │
│  │                         │                           │      │
│  │                         ▼                           │      │
│  │    Data sent SEPARATELY from SQL                     │      │
│  │    Database treats data as VALUES only               │      │
│  │    CANNOT be executed as SQL commands                │      │
│  │                                                      │      │
│  │    $stmt->execute([':id' => 2]);  ← Different ID    │      │
│  │    (Reuses prepared statement, faster!)              │      │
│  └──────────────────────────────────────────────────────┘      │
│                           │                                     │
│                           ▼                                     │
│  ┌──────────────────────────────────────────────────────┐      │
│  │ 3. FETCH RESULTS                                     │      │
│  │                                                      │      │
│  │    $user = $stmt->fetch();  // Single row           │      │
│  │    $users = $stmt->fetchAll();  // All rows         │      │
│  │                                                      │      │
│  │    Fetch modes:                                      │      │
│  │    • FETCH_ASSOC - Associative array                 │      │
│  │    • FETCH_OBJ - stdClass object                     │      │
│  │    • FETCH_CLASS - Custom class                      │      │
│  │    • FETCH_COLUMN - Single column                    │      │
│  └──────────────────────────────────────────────────────┘      │
│                                                                 │
│  ✓ SQL Injection Prevention                                     │
│  ✓ Better Performance (compiled once, executed many)            │
│  ✓ Automatic escaping of special characters                     │
│  ✓ Better readability and maintainability                       │
└─────────────────────────────────────────────────────────────────┘
```

### Connecting to Database

**Definition:** PHP connects to databases primarily using **PDO** (PHP Data Objects) or **MySQLi**. PDO is the industry standard because it supports multiple database drivers (MySQL, PostgreSQL, SQLite, etc.) with a consistent interface. It requires a DSN (Data Source Name), username, and password to establish a connection.

```php
<?php
// Database configuration
$config = [
    'driver' => 'mysql',
    'host' => 'localhost',
    'database' => 'myapp',
    'username' => 'dbuser',
    'password' => 'dbpass',
    'charset' => 'utf8mb4',
    'options' => [
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,        // Throw exceptions on errors
        PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,   // Fetch associative arrays
        PDO::ATTR_EMULATE_PREPARES => false,                // Use real prepared statements
        PDO::ATTR_PERSISTENT => true                         // Persistent connections
    ]
];

// Create connection
try {
    $dsn = "{$config['driver']}:host={$config['host']};dbname={$config['database']};charset={$config['charset']}";
    $pdo = new PDO($dsn, $config['username'], $config['password'], $config['options']);
    echo "Connected successfully";
} catch (PDOException $e) {
    error_log("Connection failed: " . $e->getMessage());
    die("Database connection failed");
}

// Connection for other databases:
// PostgreSQL: "pgsql:host=localhost;dbname=mydb"
// SQLite: "sqlite:/path/to/database.db"
// SQL Server: "sqlsrv:Server=localhost;Database=mydb"
?>
```

### Prepared Statements

**Definition:** Prepared statements are a security feature that separates the SQL query structure from the data. The database compiles the query template first, then binds the user input values later. This completely neutralizes SQL Injection attacks because the database treats user input strictly as data, never as executable code.

```php
<?php
// ALWAYS use prepared statements to prevent SQL injection!

// INSERT with prepared statement
$stmt = $pdo->prepare("INSERT INTO users (name, email, created_at) VALUES (:name, :email, NOW())");
$stmt->execute([
    ':name' => 'John Doe',
    ':email' => 'john@example.com'
]);
$userId = $pdo->lastInsertId();

// Alternative syntax (positional placeholders)
$stmt = $pdo->prepare("INSERT INTO users (name, email) VALUES (?, ?)");
$stmt->execute(['Jane Doe', 'jane@example.com']);

// SELECT with parameters
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = :id");
$stmt->execute([':id' => 1]);
$user = $stmt->fetch();  // Single row

// Multiple results
$stmt = $pdo->prepare("SELECT * FROM users WHERE status = :status");
$stmt->execute([':status' => 'active']);
$users = $stmt->fetchAll();  // All rows

// UPDATE
$stmt = $pdo->prepare("UPDATE users SET name = :name WHERE id = :id");
$stmt->execute([
    ':name' => 'John Smith',
    ':id' => 1
]);
$affectedRows = $stmt->rowCount();

// DELETE
$stmt = $pdo->prepare("DELETE FROM users WHERE id = :id");
$stmt->execute([':id' => 1]);

// Binding with explicit types
$stmt = $pdo->prepare("SELECT * FROM products WHERE price > :min_price AND category_id = :cat_id");
$stmt->bindValue(':min_price', 10.50, PDO::PARAM_STR);  // DECIMAL as string
$stmt->bindValue(':cat_id', 5, PDO::PARAM_INT);
$stmt->execute();

// Binding by reference (for loops)
$stmt = $pdo->prepare("INSERT INTO logs (message, level) VALUES (:msg, :level)");
$stmt->bindParam(':msg', $message);
$stmt->bindParam(':level', $level);

foreach ($logs as $log) {
    $message = $log['message'];
    $level = $log['level'];
    $stmt->execute();
}
?>
```

### Fetching Data

**Definition:** Fetching retrieves rows from a query result set. PDO provides `fetch()` (gets one row) and `fetchAll()` (gets all rows into an array). Fetch modes control the format: `PDO::FETCH_ASSOC` (associative array), `PDO::FETCH_OBJ` (anonymous object), and `PDO::FETCH_CLASS` (maps columns to class properties).

```php
<?php
// Different fetch modes

// Fetch associative array (default)
$stmt = $pdo->query("SELECT * FROM users");
$user = $stmt->fetch(PDO::FETCH_ASSOC);  // ['id' => 1, 'name' => 'John']

// Fetch object
$user = $stmt->fetch(PDO::FETCH_OBJ);    // stdClass with properties

// Fetch into specific class
$stmt->setFetchMode(PDO::FETCH_CLASS, 'User');
$user = $stmt->fetch();

// Fetch all
$users = $stmt->fetchAll();              // Array of arrays
$users = $stmt->fetchAll(PDO::FETCH_OBJ); // Array of objects

// Fetch column
$stmt = $pdo->query("SELECT email FROM users");
$emails = $stmt->fetchAll(PDO::FETCH_COLUMN);

// Fetch key-value pairs
$stmt = $pdo->query("SELECT id, name FROM users");
$users = $stmt->fetchAll(PDO::FETCH_KEY_PAIR);  // [1 => 'John', 2 => 'Jane']

// Fetch grouped
$stmt = $pdo->query("SELECT role, name FROM users");
$grouped = $stmt->fetchAll(PDO::FETCH_GROUP);   // Grouped by first column

// Fetching one column
$stmt = $pdo->prepare("SELECT COUNT(*) FROM users");
$stmt->execute();
$count = $stmt->fetchColumn();

// Iterate over large result sets (memory efficient)
$stmt = $pdo->query("SELECT * FROM large_table");
while ($row = $stmt->fetch()) {
    // Process one row at a time
    processRow($row);
}

// Using foreach (PDOStatement implements Traversable)
foreach ($pdo->query("SELECT * FROM users") as $user) {
    echo $user['name'];
}
?>
```

### CRUD Operations

**Definition:** CRUD stands for **Create** (INSERT), **Read** (SELECT), **Update** (UPDATE), and **Delete** (DELETE). These are the four fundamental operations of persistent storage. In PHP/PDO, these map to preparing an SQL statement and executing it with bound parameters.

```php
<?php
class UserRepository {
    private PDO $pdo;
    
    public function __construct(PDO $pdo) {
        $this->pdo = $pdo;
    }
    
    // CREATE
    public function create(array $data): int {
        $sql = "INSERT INTO users (name, email, password_hash, created_at) 
                VALUES (:name, :email, :password, NOW())";
        $stmt = $this->pdo->prepare($sql);
        $stmt->execute([
            ':name' => $data['name'],
            ':email' => $data['email'],
            ':password' => password_hash($data['password'], PASSWORD_DEFAULT)
        ]);
        return (int) $this->pdo->lastInsertId();
    }
    
    // READ
    public function find(int $id): ?array {
        $stmt = $this->pdo->prepare("SELECT * FROM users WHERE id = :id");
        $stmt->execute([':id' => $id]);
        $user = $stmt->fetch();
        return $user ?: null;
    }
    
    public function findByEmail(string $email): ?array {
        $stmt = $this->pdo->prepare("SELECT * FROM users WHERE email = :email");
        $stmt->execute([':email' => $email]);
        return $stmt->fetch() ?: null;
    }
    
    public function findAll(array $filters = []): array {
        $sql = "SELECT * FROM users WHERE 1=1";
        $params = [];
        
        if (!empty($filters['status'])) {
            $sql .= " AND status = :status";
            $params[':status'] = $filters['status'];
        }
        
        if (!empty($filters['search'])) {
            $sql .= " AND (name LIKE :search OR email LIKE :search)";
            $params[':search'] = '%' . $filters['search'] . '%';
        }
        
        $sql .= " ORDER BY created_at DESC";
        
        // Pagination
        $page = $filters['page'] ?? 1;
        $perPage = $filters['per_page'] ?? 20;
        $offset = ($page - 1) * $perPage;
        
        $sql .= " LIMIT :limit OFFSET :offset";
        $params[':limit'] = $perPage;
        $params[':offset'] = $offset;
        
        $stmt = $this->pdo->prepare($sql);
        $stmt->execute($params);
        return $stmt->fetchAll();
    }
    
    // UPDATE
    public function update(int $id, array $data): bool {
        $allowed = ['name', 'email', 'status'];
        $updates = [];
        $params = [':id' => $id];
        
        foreach ($data as $key => $value) {
            if (in_array($key, $allowed)) {
                $updates[] = "$key = :$key";
                $params[":$key"] = $value;
            }
        }
        
        if (empty($updates)) {
            return false;
        }
        
        $sql = "UPDATE users SET " . implode(', ', $updates) . " WHERE id = :id";
        $stmt = $this->pdo->prepare($sql);
        return $stmt->execute($params);
    }
    
    // DELETE
    public function delete(int $id): bool {
        $stmt = $this->pdo->prepare("DELETE FROM users WHERE id = :id");
        return $stmt->execute([':id' => $id]);
    }
    
    // Soft delete
    public function softDelete(int $id): bool {
        $stmt = $this->pdo->prepare(
            "UPDATE users SET deleted_at = NOW() WHERE id = :id"
        );
        return $stmt->execute([':id' => $id]);
    }
}
?>
```

### Transactions

**Definition:** A transaction is a sequence of database operations treated as a single atomic unit. Either all operations succeed (commit), or none do (rollback). This ensures data integrity—for example, when transferring money, deducting from one account and adding to another must both happen, or neither should.

```php
<?php
// Transactions ensure data consistency
try {
    // Start transaction
    $pdo->beginTransaction();
    
    // Execute multiple operations
    $stmt1 = $pdo->prepare("UPDATE accounts SET balance = balance - :amount WHERE id = :from");
    $stmt1->execute([':amount' => 100, ':from' => 1]);
    
    $stmt2 = $pdo->prepare("UPDATE accounts SET balance = balance + :amount WHERE id = :to");
    $stmt2->execute([':amount' => 100, ':to' => 2]);
    
    // Insert transaction record
    $stmt3 = $pdo->prepare("INSERT INTO transactions (from_account, to_account, amount) VALUES (?, ?, ?)");
    $stmt3->execute([1, 2, 100]);
    
    // Commit if all successful
    $pdo->commit();
    echo "Transfer successful";
    
} catch (Exception $e) {
    // Rollback on error
    $pdo->rollBack();
    error_log("Transaction failed: " . $e->getMessage());
    echo "Transfer failed";
}

// Savepoints (nested transactions)
try {
    $pdo->beginTransaction();
    
    // First operation
    $pdo->exec("INSERT INTO orders ...");
    $orderId = $pdo->lastInsertId();
    
    // Create savepoint
    $pdo->exec("SAVEPOINT after_order");
    
    try {
        // Risky operation
        foreach ($items as $item) {
            $pdo->prepare("INSERT INTO order_items ...")->execute([...]);
        }
    } catch (Exception $e) {
        // Rollback to savepoint, not entire transaction
        $pdo->exec("ROLLBACK TO SAVEPOINT after_order");
        // Continue with order but no items
    }
    
    $pdo->commit();
} catch (Exception $e) {
    $pdo->rollBack();
}
?>
```

---

## 14. Date & Time

### Definition
PHP provides multiple ways to work with dates and times, from simple functions to the powerful DateTime class. Understanding timezone handling, date formatting, and intervals is essential for international applications and scheduling features.

### DateTime Object Lifecycle

```
┌─────────────────────────────────────────────────────────────────┐
│              DATETIME OBJECT LIFECYCLE                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  CREATE                                                          │
│  ─────                                                           │
│  ┌──────────────────────────────────────────────────────┐      │
│  │  $date = new DateTime();          // Now            │      │
│  │  $date = new DateTime('2024-01-01 12:00:00');       │      │
│  │  $date = new DateTime('@1704067200');  // Timestamp │      │
│  │  $date = DateTime::createFromFormat('d/m/Y',        │      │
│  │                                      '01/01/2024');  │      │
│  └──────────────────────┬───────────────────────────────┘      │
│                         │                                       │
│  MANIPULATE             ▼                                       │
│  ──────────  ┌─────────────────────────────────────────┐       │
│              │                                         │       │
│              │  MODIFY:                                │       │
│              │  • $date->modify('+1 day');             │       │
│              │  • $date->modify('next Monday');        │       │
│              │  • $date->setDate(2024, 12, 25);        │       │
│              │  • $date->setTime(14, 30, 0);           │       │
│              │                                         │       │
│              │  ADD/SUBTRACT INTERVALS:                │       │
│              │  • $date->add(new DateInterval('P7D')); │       │
│              │  • $date->sub(new DateInterval('P1M'));  │       │
│              │                                         │       │
│              │  TIMEZONE:                              │       │
│              │  • $date->setTimezone($tz);             │       │
│              │                                         │       │
│              └──────────────────┬──────────────────────┘       │
│                                 │                               │
│  OUTPUT                         ▼                               │
│  ──────  ┌───────────────────────────────────────────────┐     │
│          │                                               │     │
│          │  FORMAT:                                      │     │
│          │  • $date->format('Y-m-d H:i:s');              │     │
│          │  • $date->format('l, F j, Y');                │     │
│          │                                               │     │
│          │  GET TIMESTAMP:                               │     │
│          │  • $date->getTimestamp();                     │     │
│          │                                               │     │
│          │  COMPARE:                                     │     │
│          │  • $diff = $date1->diff($date2);              │     │
│          │  • $date1 < $date2  (comparable)              │     │
│          │                                               │     │
│          └───────────────────────────────────────────────┘     │
│                                                                 │
│  INTERVAL FORMAT (DateInterval):                                │
│  • P1D = 1 day        • PT2H = 2 hours                         │
│  • P7D = 7 days       • PT30M = 30 minutes                     │
│  • P1M = 1 month      • PT1H30M = 1.5 hours                    │
│  • P1Y = 1 year        • P1Y2M3DT4H5M = 1y 2m 3d 4h 5m        │
│                                                                 │
│  IMMUTABLE ALTERNATIVE:                                         │
│  • DateTimeImmutable - returns new object on modification       │
│  • Safer functional programming style                           │
└─────────────────────────────────────────────────────────────────┘
```

### Date Functions

**Definition:** PHP's procedural date functions (`date()`, `time()`, `strtotime()`) allow simple date formatting and timestamp manipulation. `date()` formats a Unix timestamp (defaulting to "now") into a human-readable string. `strtotime()` parses English text descriptions (like "now", "+1 day") into a Unix timestamp.

```php
<?php
// Current timestamp (seconds since Unix epoch)
$timestamp = time();  // e.g., 1704067200

// Current date/time as string
echo date('Y-m-d H:i:s');  // 2024-01-01 12:30:45

// Common date formats
date('Y-m-d');          // 2024-01-01 (ISO format)
date('d/m/Y');          // 01/01/2024
date('F j, Y');         // January 1, 2024
date('l');              // Monday (full day name)
date('D');              // Mon (abbreviated day)
date('H:i:s');          // 14:30:00 (24-hour)
date('h:i:s A');        // 02:30:00 PM (12-hour)
date('c');              // 2024-01-01T12:30:45+00:00 (ISO 8601)
date('r');              // Mon, 01 Jan 2024 12:30:45 +0000 (RFC 2822)

// Format characters:
// Y - 4-digit year (2024)
// y - 2-digit year (24)
// m - Month with leading zero (01-12)
// n - Month without leading zero (1-12)
// F - Full month name (January)
// M - Abbreviated month (Jan)
// d - Day with leading zero (01-31)
// j - Day without leading zero (1-31)
// l - Full day name (Monday)
// D - Abbreviated day (Mon)
// H - 24-hour format with leading zero (00-23)
// G - 24-hour without leading zero (0-23)
// h - 12-hour with leading zero (01-12)
// i - Minutes (00-59)
// s - Seconds (00-59)
// A - AM or PM
// a - am or pm

// Convert string to timestamp
$timestamp = strtotime("2024-01-01");           // From date string
$timestamp = strtotime("+1 week");              // Relative
$timestamp = strtotime("next Monday");          // Next occurrence
$timestamp = strtotime("+3 days 2 hours");      // Complex relative

// Then format
$nextWeek = date('Y-m-d', strtotime('+1 week'));

// Check if date is valid
if (checkdate(2, 29, 2024)) {  // Month, Day, Year
    echo "2024 is a leap year";
}

// Get date parts
$date = getdate();  // Array with year, mon, mday, hours, etc.
echo $date['year'];

// Microtime (with microseconds)
echo microtime(true);  // 1704067200.123456
?>
```

### DateTime Class

**Definition:** The `DateTime` class (OOP approach) is superior to procedural date functions. It handles time zones correctly, supports date arithmetic (adding/subtracting intervals), creates immutable versions (`DateTimeImmutable`), and avoids the "Year 2038" problem on 32-bit systems. Always prefer `DateTime` over `date()` for modern applications.

```php
<?php
// Create DateTime object
$now = new DateTime();                           // Current time
$date = new DateTime('2024-01-01 12:30:00');     // From string
$date = new DateTime('@1704067200');             // From timestamp
$date = DateTime::createFromFormat('d/m/Y', '01/01/2024');

// Format output
echo $now->format('Y-m-d H:i:s');
echo $now->format('l, F j, Y');  // Monday, January 1, 2024

// Modify date
$date = new DateTime('2024-01-01');
$date->modify('+1 day');           // Add 1 day
$date->modify('+1 week');          // Add 1 week
$date->modify('-3 months');        // Subtract 3 months
$date->modify('next Monday');      // Next Monday
$date->modify('first day of next month');

// Set specific parts
$date->setDate(2024, 12, 25);      // Set date
$date->setTime(14, 30, 0);         // Set time

// Get timestamp
$timestamp = $date->getTimestamp();

// Timezone handling
$utc = new DateTimeZone('UTC');
$ny = new DateTimeZone('America/New_York');
$tokyo = new DateTimeZone('Asia/Tokyo');

$date = new DateTime('now', $utc);
echo $date->format('Y-m-d H:i:s');  // UTC time

// Convert between timezones
$date->setTimezone($ny);
echo $date->format('Y-m-d H:i:s');  // NY time

// List available timezones
$timezones = DateTimeZone::listIdentifiers();

// DateInterval - represent time periods
$interval = new DateInterval('P1D');     // 1 day
$interval = new DateInterval('P2W');     // 2 weeks
$interval = new DateInterval('P1M');     // 1 month
$interval = new DateInterval('P1Y2M3D'); // 1 year, 2 months, 3 days
$interval = new DateInterval('PT2H30M'); // 2 hours, 30 minutes

// Add/subtract intervals
$date->add($interval);
$date->sub(new DateInterval('P7D'));  // Subtract 7 days

// DatePeriod - iterate over date ranges
$start = new DateTime('2024-01-01');
$end = new DateTime('2024-12-31');
$interval = new DateInterval('P1M');  // Every month

$period = new DatePeriod($start, $interval, $end);
foreach ($period as $date) {
    echo $date->format('F Y') . "\n";
}

// Date difference
$date1 = new DateTime('2024-01-01');
$date2 = new DateTime('2024-06-15');
$diff = $date1->diff($date2);

echo $diff->format('%y years, %m months, %d days');
echo $diff->days;  // Total days

// Comparison
if ($date1 < $date2) {
    echo "Date1 is earlier";
}

// Immutable DateTime (PHP 5.5+)
$immutable = new DateTimeImmutable('2024-01-01');
$newDate = $immutable->modify('+1 day');  // Returns new object, doesn't modify original
echo $immutable->format('Y-m-d');  // Still 2024-01-01
echo $newDate->format('Y-m-d');    // 2024-01-02
?>
```

---

## 15. Include/Require

### Definition
Include and require statements allow you to insert the content of one PHP file into another, enabling code reuse and modular organization. These statements are fundamental for structuring PHP applications using separation of concerns and the DRY (Don't Repeat Yourself) principle.

### Include/Require Decision Flow

```
┌─────────────────────────────────────────────────────────────────┐
│              INCLUDE vs REQUIRE DECISION TREE                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                    START                                        │
│                      │                                          │
│                      ▼                                          │
│         ┌───────────────────────┐                              │
│         │ Is file ESSENTIAL for │                              │
│         │ script to function?   │                              │
│         └───────────┬───────────┘                              │
│                     │                                           │
│            ┌────────┴────────┐                                  │
│            │                 │                                  │
│           YES               NO                                  │
│            │                 │                                  │
│            ▼                 ▼                                  │
│    ┌──────────────┐   ┌──────────────┐                         │
│    │   REQUIRE    │   │   INCLUDE    │                         │
│    │              │   │              │                         │
│    │ • Config     │   │ • Optional   │                         │
│    │ • Core libs  │   │ • Widgets    │                         │
│    │ • Database   │   │ • Sidebar    │                         │
│    │ • Functions  │   │ • Templates  │                         │
│    └──────┬───────┘   └──────┬───────┘                         │
│           │                  │                                  │
│           ▼                  ▼                                  │
│    ┌─────────────────────────────────┐                         │
│    │    Could file be included       │                         │
│    │    multiple times?              │                         │
│    └───────────────┬─────────────────┘                         │
│                    │                                            │
│           ┌────────┴────────┐                                   │
│           │                 │                                   │
│          YES               NO                                   │
│           │                 │                                   │
│           ▼                 ▼                                   │
│    ┌─────────────┐    ┌─────────────┐                          │
│    │ REQUIRE_ONCE│    │   REQUIRE   │                          │
│    │ INCLUDE_ONCE│    │   INCLUDE   │                          │
│    │             │    │             │                          │
│    │ Use for:    │    │ Use when:   │                          │
│    │ • Class def │    │ intentional │                          │
│    │ • Functions │    │ multiple    │                          │
│    │ • Config    │    │ includes    │                          │
│    └─────────────┘    └─────────────┘                          │
│                                                                 │
│  FILE LOOKUP ORDER:                                             │
│  1. Absolute path (if provided)                                 │
│  2. Include path (php.ini setting)                              │
│  3. Script's directory and current working directory            │
│                                                                 │
│  BEST PRACTICE:                                                 │
│  • Use absolute paths: require __DIR__ . '/file.php';          │
│  • Use _ONCE for classes/functions to avoid redeclaration       │
│  • Autoload classes with Composer instead of manual includes    │
└─────────────────────────────────────────────────────────────────┘
```

### Include vs Require

**Definition:** `include` and `require` insert the content of one PHP file into another. The difference is their failure behavior: `include` emits a warning but continues execution if the file is missing; `require` emits a fatal error and stops script execution. `_once` versions (e.g., `require_once`) ensure the file is loaded only once, preventing re-declaration errors.

```php
<?php
// include - includes file, warning if not found (script continues)
include 'header.php';

// require - includes file, fatal error if not found (script stops)
require 'config.php';

// include_once - includes only if not already included
include_once 'functions.php';

// require_once - requires only if not already required
require_once 'database.php';

// Use _once versions for:
// - Function definitions
// - Class definitions
// - Configuration files
// To prevent "already defined" errors

// Best practice: Use require for essential files
require 'vendor/autoload.php';  // Essential
require 'database/config.php';   // Essential

// Use include for optional components
include 'optional-widget.php';   // Optional
include 'sidebar-' . $layout . '.php';  // Dynamic

// Return values from included files
// config.php:
// <?php return ['db_host' => 'localhost', 'db_name' => 'myapp'];

$config = require 'config.php';
echo $config['db_host'];
?>
```

### Autoloading

**Definition:** Autoloading allows PHP to automatically load class files when they are needed, eliminating the need for manual `require` statements. Composer provides a standard autoloader (based on PSR-4) that maps namespaces to directory paths. You simply require `vendor/autoload.php` once, and classes load on demand.

```php
<?php
// Manual autoloader
spl_autoload_register(function ($class) {
    // Convert namespace separators to directory separators
    $file = str_replace('\\', '/', $class) . '.php';
    
    // PSR-4 style: Vendor\Package\Class -> vendor/package/Class.php
    $file = 'src/' . $file;
    
    if (file_exists($file)) {
        require $file;
    }
});

// Composer autoloader (preferred)
require 'vendor/autoload.php';

// Use classes
$user = new App\Models\User();
$controller = new App\Controllers\HomeController();
?>
```

### Project Structure

**Definition:** A standard PHP project structure improves organization and maintainability. It typically separates public assets (`public/`), source code (`src/` or `app/`), vendor libraries (`vendor/`), configuration (`config/`), and views (`views/` or `templates/`). The `public/index.php` file usually serves as the single entry point (Front Controller).

```php
<?php
// Recommended project structure:
/*
project/
├── public/                 # Web root (document root)
│   ├── index.php          # Front controller
│   ├── .htaccess          # Apache rewrite rules
│   ├── css/
│   ├── js/
│   └── images/
├── src/                   # Application code
│   ├── Controllers/
│   ├── Models/
│   ├── Views/
│   ├── Services/
│   └── Utils/
├── config/                # Configuration files
│   ├── database.php
│   └── app.php
├── vendor/                # Composer dependencies
├── tests/                 # Test files
├── storage/               # Logs, cache, uploads
│   ├── logs/
│   ├── cache/
│   └── uploads/
└── composer.json
*/

// public/index.php (front controller)
<?php
require_once __DIR__ . '/../vendor/autoload.php';
require_once __DIR__ . '/../config/app.php';

// Initialize application
$app = new App\Application();
$app->run();

// config/database.php
<?php
return [
    'driver' => 'mysql',
    'host' => $_ENV['DB_HOST'] ?? 'localhost',
    'database' => $_ENV['DB_NAME'] ?? 'myapp',
    'username' => $_ENV['DB_USER'] ?? 'root',
    'password' => $_ENV['DB_PASS'] ?? '',
    'charset' => 'utf8mb4',
];

// bootstrap.php
<?php
// Load configuration
$config = require __DIR__ . '/config/app.php';
$dbConfig = require __DIR__ . '/config/database.php';

// Initialize database
$pdo = new PDO(
    "mysql:host={$dbConfig['host']};dbname={$dbConfig['database']}",
    $dbConfig['username'],
    $dbConfig['password']
);

// Make available globally or via dependency injection
$GLOBALS['pdo'] = $pdo;
?>
```

---

## 🔑 Key Takeaways

1. **Security First**: Always validate and sanitize user input, use prepared statements for database queries, escape output with `htmlspecialchars()`
2. **Modern PHP**: Use PHP 8+ features like named arguments, match expressions, union types, nullsafe operator, and attributes
3. **Error Handling**: Use exceptions for error handling, never expose sensitive error details in production
4. **Database Best Practices**: Always use PDO with prepared statements, use transactions for multi-step operations
5. **Session Security**: Regenerate IDs on login, use httponly and secure flags for cookies, implement CSRF protection
6. **File Handling**: Validate file types and sizes, generate safe filenames, never trust user-provided filenames
7. **Code Organization**: Use autoloading (Composer), separate concerns (MVC pattern), keep configuration out of version control

---

**Next:** Practice building a complete PHP application combining forms, database operations, and sessions!