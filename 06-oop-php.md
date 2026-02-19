# 🐘 Object-Oriented Programming (OOP) in PHP

## Summary

This document covers Object-Oriented Programming in PHP. Topics include the four pillars of OOP (encapsulation, abstraction, inheritance, polymorphism), classes and objects, access modifiers, inheritance with abstract classes and final keyword, interfaces, traits for code reuse, static methods and properties, magic methods, namespaces and autoloading, dependency injection, design patterns, SOLID principles, and modern PHP 8+ features.

## Sommaire

- [📊 UML Introduction](#📊-uml-introduction)
  - [Four Pillars of OOP](#four-pillars-of-oop)
  - [Class vs Object](#class-vs-object)
- [1. Introduction to OOP](#1-introduction-to-oop)
  - [Definition](#definition)
  - [Four Pillars of OOP](#four-pillars-of-oop)
  - [Procedural vs OOP](#procedural-vs-oop)
  - [Benefits of OOP](#benefits-of-oop)
- [2. Classes & Objects](#2-classes-&-objects)
  - [Definition](#definition)
  - [Simple Class Diagram](#simple-class-diagram)
  - [Defining Classes](#defining-classes)
  - [Constructor Property Promotion (PHP 8+)](#constructor-property-promotion-php-8+)
  - [The $this Keyword](#the-$this-keyword)
  - [Best Practices](#best-practices)
- [3. Access Modifiers & Encapsulation](#3-access-modifiers-&-encapsulation)
  - [Definition](#definition)
  - [Encapsulation Diagram](#encapsulation-diagram)
  - [Access Modifiers](#access-modifiers)
  - [Readonly Properties (PHP 8.1+)](#readonly-properties-php-81+)
  - [Constructor with Readonly (PHP 8.1+)](#constructor-with-readonly-php-81+)
  - [Encapsulation Benefits](#encapsulation-benefits)
- [4. Inheritance](#4-inheritance)
  - [Definition](#definition)
  - [Inheritance Hierarchy Diagram](#inheritance-hierarchy-diagram)
  - [extends Keyword](#extends-keyword)
  - [Final Keyword](#final-keyword)
  - [Abstract Classes](#abstract-classes)
  - [Inheritance vs Composition](#inheritance-vs-composition)
  - [Best Practices](#best-practices)
- [5. Polymorphism](#5-polymorphism)
  - [Definition](#definition)
  - [Polymorphism Diagram](#polymorphism-diagram)
  - [Method Overriding](#method-overriding)
  - [Type Hinting](#type-hinting)
  - [Practical Example: Plugin System](#practical-example-plugin-system)
- [6. Interfaces](#6-interfaces)
  - [Definition](#definition)
  - [Interface Implementation Diagram](#interface-implementation-diagram)
  - [Defining Interfaces](#defining-interfaces)
  - [Multiple Interfaces](#multiple-interfaces)
  - [Interface vs Abstract Class](#interface-vs-abstract-class)
- [7. Traits](#7-traits)
  - [Definition](#definition)
  - [Trait Composition Diagram](#trait-composition-diagram)
  - [Defining Traits](#defining-traits)
  - [Conflict Resolution](#conflict-resolution)
  - [Trait Properties](#trait-properties)
  - [When to Use Traits](#when-to-use-traits)
- [8. Static Methods & Properties](#8-static-methods-&-properties)
  - [Definition](#definition)
  - [Static Members Diagram](#static-members-diagram)
  - [Static Keyword](#static-keyword)
  - [self:: vs static:: (Late Static Binding)](#self-vs-static-late-static-binding)
  - [Practical Example: Counter](#practical-example-counter)
  - [When to Use Static](#when-to-use-static)
  - [Avoid](#avoid)
- [9. Magic Methods](#9-magic-methods)
  - [Definition](#definition)
  - [Magic Methods Overview](#magic-methods-overview)
  - [Magic Methods Reference](#magic-methods-reference)
  - [Common Magic Methods](#common-magic-methods)
  - [Practical Example: Array-like Object](#practical-example-array-like-object)
  - [Serialization Magic Methods](#serialization-magic-methods)
- [10. Namespaces & Autoloading](#10-namespaces-&-autoloading)
  - [Definition](#definition)
  - [Namespace Structure Diagram](#namespace-structure-diagram)
  - [namespace Keyword](#namespace-keyword)
  - [PSR-4 Autoloading](#psr-4-autoloading)
  - [Custom Autoloader](#custom-autoloader)
  - [Best Practices](#best-practices)
- [11. Dependency Injection](#11-dependency-injection)
  - [Definition](#definition)
  - [Dependency Injection Pattern Diagram](#dependency-injection-pattern-diagram)
  - [What is DI](#what-is-di)
  - [Constructor Injection (Preferred)](#constructor-injection-preferred)
  - [Interface-Based Injection](#interface-based-injection)
  - [Composition Over Inheritance](#composition-over-inheritance)
- [12. Design Patterns](#12-design-patterns)
  - [Definition](#definition)
  - [Singleton Pattern](#singleton-pattern)
  - [Factory Pattern](#factory-pattern)
  - [MVC Overview](#mvc-overview)
- [13. SOLID Principles](#13-solid-principles)
  - [Definition](#definition)
  - [Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
  - [Open/Closed Principle (OCP)](#open/closed-principle-ocp)
  - [Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
  - [Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
  - [Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)
- [14. PHP 8+ OOP Features](#14-php-8+-oop-features)
  - [Definition](#definition)
  - [Constructor Property Promotion](#constructor-property-promotion)
  - [Named Arguments](#named-arguments)
  - [Match Expression](#match-expression)
  - [Union Types](#union-types)
  - [Nullsafe Operator](#nullsafe-operator)
  - [Enums (PHP 8.1+)](#enums-php-81+)
  - [Readonly Classes (PHP 8.2+)](#readonly-classes-php-82+)
  - [Intersection Types (PHP 8.1+)](#intersection-types-php-81+)
  - [First-Class Callable Syntax (PHP 8.1+)](#first-class-callable-syntax-php-81+)
- [🔑 Key Takeaways](#🔑-key-takeaways)



> Object-Oriented Programming is a paradigm that organizes code around objects rather than functions and logic. PHP provides robust OOP features for building scalable, maintainable applications.

---

## 📊 UML Introduction

### Four Pillars of OOP

```
┌─────────────────────────────────────────────────────────────────┐
│                   FOUR PILLARS OF OOP                           │
├─────────────────┬─────────────────┬─────────────────┬───────────┤
│  ENCAPSULATION  │   ABSTRACTION   │   INHERITANCE   │ POLYMORPH │
├─────────────────┼─────────────────┼─────────────────┼───────────┤
│ • Data hiding   │ • Hide complex  │ • Create new    │ • Same     │
│ • Private props │   details       │   classes from  │   interface│
│ • Public methods│ • Show only     │   existing ones │   different│
│ • Controlled    │   essentials    │ • "is-a"        │   behavior │
│   access        │                 │   relationship  │            │
└─────────────────┴─────────────────┴─────────────────┴───────────┘
```

### Class vs Object

**Definition:** A **Class** is a blueprint or template that defines the properties (variables) and methods (functions) common to all objects of that type. An **Object** is an instance of a class — a concrete entity created based on the blueprint, with its own specific data.

```
┌─────────────────────────────────────────────────────────────────┐
│                     CLASS vs OBJECT                             │
├────────────────────────────────┬────────────────────────────────┤
│            CLASS               │            OBJECT              │
├────────────────────────────────┼────────────────────────────────┤
│ • Blueprint/Template           │ • Instance of a class          │
│ • Abstract definition          │ • Concrete entity              │
│ • No memory allocation         │ • Memory allocated             │
│ • Declared with "class"        │ • Created with "new"           │
├────────────────────────────────┼────────────────────────────────┤
│      car                       │   $myCar = new Car();          │
│  ┌───────────────┐             │   ┌───────────────┐            │
│  │     Car       │             │   │     Car       │            │
│  ├───────────────┤             │   ├───────────────┤            │
│  │ - brand       │  ───────►   │   │ - brand: BMW  │            │
│  │ - color       │   instanti- │   │ - color: Blue │            │
│  ├───────────────┤   ation     │   ├───────────────┤            │
│  │ + drive()     │             │   │ + drive()     │            │
│  │ + brake()     │             │   │ + brake()     │            │
│  └───────────────┘             │   └───────────────┘            │
│                                │   Memory address: 0x7F3A       │
└────────────────────────────────┴────────────────────────────────┘
```

---

## 1. Introduction to OOP

### Definition

**Object-Oriented Programming (OOP)** is a programming paradigm based on the concept of **objects**, which contain data (properties) and code (methods). Objects are instances of **classes**, which serve as blueprints.

- **Class**: A template or blueprint defining properties and methods
- **Object**: A concrete instance of a class with actual values
- **Property**: A variable that belongs to a class (also called attribute or field)
- **Method**: A function that belongs to a class and operates on its data

### Four Pillars of OOP

| Pillar | Description |
|--------|-------------|
| **Encapsulation** | Bundling data and methods that work on that data within one unit, restricting direct access to some components |
| **Abstraction** | Hiding complex implementation details and showing only essential features |
| **Inheritance** | Creating new classes from existing ones, promoting code reuse |
| **Polymorphism** | Ability of different objects to respond to the same method call in different ways |

### Procedural vs OOP

**Definition:** Procedural programming performs tasks in sequential steps (functions operating on data). Object-Oriented Programming (OOP) organizes code into objects (data + behavior combined). Procedural is simpler for small scripts; OOP manages complexity better in large applications by modularizing code and managing state.

```php
<?php
// Procedural approach - functions and global data
$users = [];

function createUser($name, $email) {
    global $users;
    $users[] = ['name' => $name, 'email' => $email];
}

function getUserEmail($name) {
    global $users;
    foreach ($users as $user) {
        if ($user['name'] === $name) {
            return $user['email'];
        }
    }
    return null;
}

createUser('John', 'john@example.com');
echo getUserEmail('John');
?>
```

```php
<?php
// OOP approach - encapsulation and organization
class User {
    private string $name;
    private string $email;
    
    public function __construct(string $name, string $email) {
        $this->name = $name;
        $this->email = $email;
    }
    
    public function getEmail(): string {
        return $this->email;
    }
}

class UserRepository {
    private array $users = [];
    
    public function add(User $user): void {
        $this->users[] = $user;
    }
    
    public function findByName(string $name): ?User {
        foreach ($this->users as $user) {
            if ($user->getName() === $name) {
                return $user;
            }
        }
        return null;
    }
}

$repo = new UserRepository();
$repo->add(new User('John', 'john@example.com'));
?>
```

### Benefits of OOP

**Definition:** The primary benefits of OOP are modularity (easier troubleshooting), reusability (inheritance/polymorphism reduces duplication), productivity (classes can be reused across projects), and maintainability (changes in a class logic don't break other parts of the system if the interface remains the same).
- **Modularity** - Code organized into self-contained objects
- **Reusability** - Inheritance and composition enable code reuse
- **Maintainability** - Easier to modify and debug
- **Scalability** - Better suited for large applications
- **Collaboration** - Teams can work on different classes simultaneously

---

## 2. Classes & Objects

### Definition

**Class**: A template/blueprint that defines properties and methods for objects. Think of it as a recipe for creating objects.

**Object**: An instance of a class created with the `new` keyword. Objects have state (property values) and behavior (methods).

**Constructor**: A special method called automatically when an object is created, used to initialize properties.

**Destructor**: A special method called automatically when an object is destroyed, used for cleanup.

### Simple Class Diagram

```
┌─────────────────────────────────────────────────────┐
│                      Car                            │
├─────────────────────────────────────────────────────┤
│ - brand: string    (private)                        │
│ - model: string    (private)                        │
│ - year: int        (private)                        │
│ - mileage: float   (protected)                      │
├─────────────────────────────────────────────────────┤
│ + __construct(brand, model, year)                   │
│ + drive(distance: float): void                      │
│ + getAge(): int                                     │
│ + getMileage(): float                               │
│ - calculateDepreciation(): float  (private)         │
└─────────────────────────────────────────────────────┘

Notation:
- "-" = private (accessible only within class)
- "+" = public  (accessible from anywhere)
- "#" = protected (accessible within class and subclasses)
```

### Defining Classes

```php
<?php
// Basic class definition
class Car {
    // Properties (attributes)
    public string $brand;
    public string $model;
    private int $year;
    protected float $mileage = 0;
    
    // Class constant
    public const WHEELS = 4;
    
    // Constructor
    public function __construct(string $brand, string $model, int $year) {
        $this->brand = $brand;
        $this->model = $model;
        $this->year = $year;
    }
    
    // Methods
    public function drive(float $distance): void {
        $this->mileage += $distance;
        echo "Drove {$distance} km. Total: {$this->mileage} km\n";
    }
    
    public function getAge(): int {
        return date('Y') - $this->year;
    }
    
    // Destructor - called when object is destroyed
    public function __destruct() {
        echo "Car {$this->brand} {$this->model} is being destroyed\n";
    }
}

// Creating objects (instances)
$myCar = new Car('Toyota', 'Corolla', 2020);
$yourCar = new Car('Honda', 'Civic', 2022);

// Accessing properties and methods
echo $myCar->brand;          // Toyota
echo Car::WHEELS;            // 4 (access constant)
$myCar->drive(100);          // Drove 100 km
echo $myCar->getAge();       // 4 (assuming current year is 2024)

// Using instanceof
if ($myCar instanceof Car) {
    echo "This is a Car object\n";
}
?>
```

### Constructor Property Promotion (PHP 8+)

**Definition:** Constructor property promotion significantly reduces boilerplate code by allowing you to declare and initialize class properties directly in the constructor signature. It combines the property declaration, constructor argument, and property assignment into a single syntax.

```php
<?php
// Before PHP 8 - verbose
class Product {
    private string $name;
    private float $price;
    private int $stock;
    
    public function __construct(string $name, float $price, int $stock) {
        $this->name = $name;
        $this->price = $price;
        $this->stock = $stock;
    }
}

// PHP 8+ - Constructor Property Promotion
class Product {
    public function __construct(
        private string $name,
        private float $price,
        private int $stock = 0  // Default value supported
    ) {}
    
    public function getName(): string {
        return $this->name;
    }
}

$product = new Product('Laptop', 999.99, 10);
?>
```

### The $this Keyword

**Definition:** `$this` is a pseudo-variable available inside class methods that refers to the current object instance. It is used to access the object's properties and methods from within the object itself. You cannot use `$this` inside static methods.

```php
<?php
class Person {
    private string $firstName;
    private string $lastName;
    
    public function __construct(string $firstName, string $lastName) {
        // $this refers to the current object instance
        $this->firstName = $firstName;
        $this->lastName = $lastName;
    }
    
    public function getFullName(): string {
        // Accessing properties with $this
        return $this->firstName . ' ' . $this->lastName;
    }
    
    public function greet(): string {
        // Calling another method with $this
        return 'Hello, I am ' . $this->getFullName();
    }
}

$person = new Person('John', 'Doe');
echo $person->greet();  // Hello, I am John Doe
?>
```

### Best Practices
- Use constructor property promotion for cleaner code (PHP 8+)
- Keep constructors simple - avoid heavy logic
- Use type declarations for all parameters and return types
- Initialize properties in constructor, not at declaration for complex types

---

## 3. Access Modifiers & Encapsulation

### Definition

**Encapsulation**: The bundling of data (properties) and methods that operate on that data within a single unit (class), while restricting direct access to some of the object's components.

**Access Modifiers**: Keywords that control the visibility of properties and methods:
- `public`: Accessible from anywhere
- `protected`: Accessible within the class and its subclasses
- `private`: Accessible only within the class itself

**Getters/Setters**: Methods that provide controlled read/write access to private properties.

**Readonly**: Properties that can only be initialized once and then become immutable.

### Encapsulation Diagram

```
┌────────────────────────────────────────────────────────────┐
│                    BankAccount                             │
├────────────────────────────────────────────────────────────┤
│ PRIVATE:                                                   │
│   - balance: float = 0      <-- Internal state             │
│   - accountNumber: string                                  │
│ PROTECTED:                                                 │
│   # accountType: string                                    │
│ PUBLIC:                                                    │
│   + ownerName: string       <-- External access            │
├────────────────────────────────────────────────────────────┤
│ PUBLIC METHODS:                                            │
│   + getBalance(): float     <-- Read via method            │
│   + deposit(amount): void   <-- Write with validation      │
│   + withdraw(amount): void                                 │
│                                                            │
│ Encapsulation Benefit:                                     │
│   External code --> public methods --> private data        │
│   (cannot modify balance directly)                         │
└────────────────────────────────────────────────────────────┘
```

### Access Modifiers

```php
<?php
class BankAccount {
    // Private - accessible only within this class
    private float $balance = 0;
    private string $accountNumber;
    
    // Protected - accessible within class and child classes
    protected string $accountType = 'checking';
    
    // Public - accessible from anywhere
    public string $ownerName;
    
    public function __construct(string $ownerName, string $accountNumber) {
        $this->ownerName = $ownerName;
        $this->accountNumber = $accountNumber;
    }
    
    // Getter method - controlled access to private property
    public function getBalance(): float {
        return $this->balance;
    }
    
    // Setter method - controlled modification with validation
    public function deposit(float $amount): void {
        if ($amount <= 0) {
            throw new InvalidArgumentException('Amount must be positive');
        }
        $this->balance += $amount;
    }
    
    public function withdraw(float $amount): void {
        if ($amount > $this->balance) {
            throw new RuntimeException('Insufficient funds');
        }
        $this->balance -= $amount;
    }
}

$account = new BankAccount('John Doe', '123456789');

// Public property - direct access
$account->ownerName = 'Jane Doe';

// Private property - must use methods
// $account->balance = 1000;  // ERROR!
$account->deposit(1000);
echo $account->getBalance();  // 1000
?>
```

### Readonly Properties (PHP 8.1+)

**Definition:** `readonly` properties can only be initialized once and cannot be modified thereafter. They provide immutability guarantees directly at the language level. A readonly property must be typed and cannot have a default value (except in the constructor).

```php
<?php
class UserProfile {
    // Readonly - can be initialized once, then immutable
    public readonly string $id;
    public readonly string $email;
    public string $displayName;  // Not readonly - can change
    
    public function __construct(string $id, string $email) {
        $this->id = $id;        // Initialized in constructor
        $this->email = $email;  // Initialized in constructor
    }
    
    public function updateEmail(string $newEmail): void {
        // $this->email = $newEmail;  // ERROR! Cannot modify readonly property
    }
}

$user = new UserProfile('user-123', 'john@example.com');
$user->displayName = 'John';  // OK - not readonly
// $user->id = 'user-456';     // ERROR! Readonly property
?>
```

### Constructor with Readonly (PHP 8.1+)

**Definition:** You can combine constructor property promotion with the `readonly` modifier to create immutable Data Transfer Objects (DTOs) with minimal syntax. This is the modern PHP standard for value objects that should not change after creation.

```php
<?php
class Order {
    public function __construct(
        public readonly string $orderId,
        public readonly float $total,
        public readonly DateTimeImmutable $createdAt,
        private string $status = 'pending'
    ) {}
    
    public function getStatus(): string {
        return $this->status;
    }
    
    public function setStatus(string $status): void {
        $this->status = $status;  // OK - status is not readonly
    }
}

$order = new Order('ORD-001', 99.99, new DateTimeImmutable());
// $order->total = 199.99;  // ERROR! Readonly property
?>
```

### Encapsulation Benefits

**Definition:** Encapsulation hides the internal state of an object and requires all interaction to be performed through an object's methods. This protects the data integrity (preventing invalid states), creates a clear API boundary, and allows the implementation to change without affecting dependent code.
- **Data hiding** - Internal state protected from external modification
- **Validation** - Control what values are allowed through setters
- **Flexibility** - Change internal implementation without affecting external code
- **Debugging** - Centralized control over data access

---

## 4. Inheritance

### Definition

**Inheritance**: A mechanism where a new class (child/subclass) derives properties and methods from an existing class (parent/superclass). It represents an "is-a" relationship.

**extends**: The keyword used to create a subclass that inherits from a parent class.

**parent::**: Used to call methods from the parent class.

**Override**: Replacing a parent method with a new implementation in the child class.

**final**: Prevents a class from being inherited or a method from being overridden.

**Abstract Class**: A class that cannot be instantiated and may contain abstract methods that must be implemented by subclasses.

### Inheritance Hierarchy Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                      Animal                                 │
│                     (Parent)                                │
├─────────────────────────────────────────────────────────────┤
│ # name: string                                              │
│ # age: int                                                  │
├─────────────────────────────────────────────────────────────┤
│ + __construct(name, age)                                    │
│ + speak(): string                                           │
│ + getInfo(): string                                         │
└──────────────────────────┬──────────────────────────────────┘
                           │ extends
           ┌───────────────┴───────────────┐
           |                               |
           v                               v
┌───────────────────────┐     ┌───────────────────────┐
│         Dog           │     │         Cat           │
│       (Child)         │     │       (Child)         │
├───────────────────────┤     ├───────────────────────┤
│ - breed: string       │     │ - isIndoor: bool      │
├───────────────────────┤     ├───────────────────────┤
│ + __construct(...)    │     │ + __construct(...)    │
│ + speak(): string     │     │ + speak(): string     │
│ + fetch(): string     │     │ + climb(): string     │
│ + getInfo(): string   │     │ + getInfo(): string   │
└───────────────────────┘     └───────────────────────┘

"Dog IS-A Animal"       "Cat IS-A Animal"
Dog inherits:           Cat inherits:
  - name, age             - name, age
  - getInfo()             - getInfo()
  - Overrides speak()     - Overrides speak()
```

### extends Keyword

**Definition:** The `extends` keyword is used to establish an inheritance relationship between two classes. The child class (subclass) inherits all public and protected properties and methods from the parent class (superclass), allowing it to reuse and extend the parent's functionality.

```php
<?php
// Parent/Base class
class Animal {
    protected string $name;
    protected int $age;
    
    public function __construct(string $name, int $age) {
        $this->name = $name;
        $this->age = $age;
    }
    
    public function speak(): string {
        return 'Some sound';
    }
    
    public function getInfo(): string {
        return "{$this->name} is {$this->age} years old";
    }
}

// Child/Derived class
class Dog extends Animal {
    private string $breed;
    
    public function __construct(string $name, int $age, string $breed) {
        // Call parent constructor
        parent::__construct($name, $age);
        $this->breed = $breed;
    }
    
    // Override parent method
    public function speak(): string {
        return 'Woof! Woof!';
    }
    
    public function fetch(): string {
        return "{$this->name} is fetching the ball";
    }
    
    // Extend parent method
    public function getInfo(): string {
        return parent::getInfo() . " (Breed: {$this->breed})";
    }
}

class Cat extends Animal {
    public function speak(): string {
        return 'Meow!';
    }
    
    public function climb(): string {
        return "{$this->name} is climbing";
    }
}

// Usage
$dog = new Dog('Buddy', 3, 'Golden Retriever');
echo $dog->speak();       // Woof! Woof!
echo $dog->fetch();       // Buddy is fetching the ball
echo $dog->getInfo();     // Buddy is 3 years old (Breed: Golden Retriever)

$cat = new Cat('Whiskers', 2);
echo $cat->speak();       // Meow!
?>
```

### Final Keyword

**Definition:** The `final` keyword prevents a class from being inherited (`final class`) or a method from being overridden (`final function`). It is used to enforce security or design intent, ensuring that a critical implementation cannot be modified by subclasses.

```php
<?php
// Prevent class from being inherited
final class Config {
    public const APP_NAME = 'MyApp';
    public const VERSION = '1.0.0';
}

// class ExtendedConfig extends Config {}  // ERROR!

class Database {
    // Prevent method from being overridden
    final public function connect(): void {
        // Connection logic
    }
    
    // This can be overridden
    public function query(string $sql): array {
        return [];
    }
}

class MySQLDatabase extends Database {
    // public function connect(): void {}  // ERROR! Cannot override final method
    
    public function query(string $sql): array {
        // MySQL-specific implementation
        return parent::query($sql);
    }
}
?>
```

### Abstract Classes

```php
<?php
// Abstract class - cannot be instantiated
abstract class Shape {
    protected string $color;
    
    public function __construct(string $color) {
        $this->color = $color;
    }
    
    // Abstract method - must be implemented by child classes
    abstract public function getArea(): float;
    abstract public function getPerimeter(): float;
    
    // Concrete method - can be used as-is or overridden
    public function getColor(): string {
        return $this->color;
    }
}

class Circle extends Shape {
    private float $radius;
    
    public function __construct(string $color, float $radius) {
        parent::__construct($color);
        $this->radius = $radius;
    }
    
    public function getArea(): float {
        return pi() * $this->radius ** 2;
    }
    
    public function getPerimeter(): float {
        return 2 * pi() * $this->radius;
    }
}

class Rectangle extends Shape {
    private float $width;
    private float $height;
    
    public function __construct(string $color, float $width, float $height) {
        parent::__construct($color);
        $this->width = $width;
        $this->height = $height;
    }
    
    public function getArea(): float {
        return $this->width * $this->height;
    }
    
    public function getPerimeter(): float {
        return 2 * ($this->width + $this->height);
    }
}

// $shape = new Shape('red');  // ERROR! Cannot instantiate abstract class
$circle = new Circle('red', 5);
echo $circle->getArea();  // 78.54...
?>
```

### Inheritance vs Composition

**Definition:** Inheritance ("is-a" relationship) allows code reuse through hierarchy but can create tight coupling and rigid structures. Composition ("has-a" relationship) builds complex objects by combining simpler objects (dependencies). Composition is generally preferred over deep inheritance hierarchies for better flexibility and testability.

```php
<?php
// INHERITANCE - "is-a" relationship
class Vehicle {
    protected string $brand;
    protected float $speed = 0;
}

class Car extends Vehicle {
    private int $trunkCapacity;
}

// COMPOSITION - "has-a" relationship (preferred in most cases)
class Engine {
    public function start(): void {}
    public function stop(): void {}
}

class Wheels {
    public function rotate(): void {}
}

class CarComposition {
    private Engine $engine;      // Car HAS an Engine
    private Wheels $wheels;      // Car HAS Wheels
    private string $brand;
    
    public function __construct() {
        $this->engine = new Engine();
        $this->wheels = new Wheels();
    }
    
    public function start(): void {
        $this->engine->start();
    }
    
    public function drive(): void {
        $this->wheels->rotate();
    }
}

// Dependency Injection (better composition)
class CarWithDI {
    public function __construct(
        private Engine $engine,
        private Wheels $wheels,
        private string $brand
    ) {}
    
    public function start(): void {
        $this->engine->start();
    }
}

// Usage with DI
$engine = new ElectricEngine();
$wheels = new SportsWheels();
$car = new CarWithDI($engine, $wheels, 'Tesla');
?>
```

### Best Practices
- **Favor composition over inheritance** - More flexible and testable
- Use inheritance for true "is-a" relationships
- Keep inheritance hierarchies shallow (max 2-3 levels)
- Use abstract classes for shared implementation
- Mark classes/methods `final` by default, remove when needed

---

## 5. Polymorphism

### Definition

**Polymorphism**: The ability of different objects to respond to the same method call in different ways. It allows objects of different classes to be treated as objects of a common parent class, with each implementing methods differently.

**Method Overriding**: When a child class provides a different implementation of a method defined in its parent class.

**Type Hinting**: Specifying the expected type of a parameter, allowing polymorphic behavior through interfaces or parent classes.

**Dynamic Dispatch**: The process by which the correct method implementation is selected at runtime based on the object's actual type.

### Polymorphism Diagram

```
┌──────────────────────────────────────────────────────────────────┐
│                    Polymorphism                                  │
│              (Many Forms, Same Interface)                        │
└──────────────────────────────────────────────────────────────────┘
                             │
                             ▼
           ┌────────────────────────────────┐
           │     PaymentProcessor           │
           │     (Parent/Interface)         │
           ├────────────────────────────────┤
           │ + process(amount): string      │
           └────────────────┬───────────────┘
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        v                 v                 v
┌───────────────┐ ┌───────────────┐ ┌───────────────┐
│ StripeProcessor│ │ PayPalProcessor│ │ BankProcessor  │
├───────────────┤ ├───────────────┤ ├───────────────┤
│+process()     │ │+process()     │ │+process()     │
│"Stripe API"   │ │"PayPal API"   │ │"Bank Transfer"│
└───────────────┘ └───────────────┘ └───────────────┘
        │                 │                 │
        └─────────────────┼─────────────────┘
                          │
                          ▼
              checkout($processor, $amount)
              // Works with ANY PaymentProcessor
```

### Method Overriding

**Definition:** Method overriding occurs when a child class allows defines a method with the same name and arguments as a method in its parent class. The child's implementation replaces the parent's when called on an instance of the child. You can access the parent's original method using `parent::methodName()`.

```php
<?php
class PaymentProcessor {
    public function process(float $amount): string {
        return "Processing \${$amount} payment";
    }
}

class StripeProcessor extends PaymentProcessor {
    public function process(float $amount): string {
        // Different implementation for Stripe
        return "Processing \${$amount} via Stripe API";
    }
}

class PayPalProcessor extends PaymentProcessor {
    public function process(float $amount): string {
        // Different implementation for PayPal
        return "Processing \${$amount} via PayPal API";
    }
}

// Polymorphism in action
function checkout(PaymentProcessor $processor, float $amount): void {
    echo $processor->process($amount) . "\n";
}

$stripe = new StripeProcessor();
$paypal = new PayPalProcessor();

checkout($stripe, 100.00);  // Processing $100 via Stripe API
checkout($paypal, 50.00);   // Processing $50 via PayPal API
?>
```

### Type Hinting

**Definition:** Type hinting (declarations) explicitly specifies the expected data type of function arguments and return values. This enforces strict contracts between components, catches errors early (at call time), and improves code readability and IDE support. PHP supports scalar types, class names, interfaces, and union types.

```php
<?php
interface Notifiable {
    public function send(string $message): bool;
}

class EmailNotification implements Notifiable {
    public function __construct(private string $email) {}
    
    public function send(string $message): bool {
        echo "Sending email to {$this->email}: {$message}\n";
        return true;
    }
}

class SmsNotification implements Notifiable {
    public function __construct(private string $phone) {}
    
    public function send(string $message): bool {
        echo "Sending SMS to {$this->phone}: {$message}\n";
        return true;
    }
}

class PushNotification implements Notifiable {
    public function __construct(private string $deviceId) {}
    
    public function send(string $message): bool {
        echo "Sending push notification to {$this->deviceId}: {$message}\n";
        return true;
    }
}

// Polymorphic function - works with any Notifiable
function notifyUser(Notifiable $notification, string $message): void {
    $notification->send($message);
}

// Works with any implementation
$email = new EmailNotification('user@example.com');
$sms = new SmsNotification('+1234567890');
$push = new PushNotification('device-123');

notifyUser($email, 'Welcome!');
notifyUser($sms, 'Your code is 1234');
notifyUser($push, 'New message received');
?>
```

### Practical Example: Plugin System

```php
<?php
abstract class Plugin {
    protected string $name;
    protected bool $active = true;
    
    abstract public function execute(): void;
    
    public function isActive(): bool {
        return $this->active;
    }
}

class LoggingPlugin extends Plugin {
    public function execute(): void {
        echo "[LOG] Executing logging plugin\n";
    }
}

class CachingPlugin extends Plugin {
    public function execute(): void {
        echo "[CACHE] Clearing cache\n";
    }
}

class SecurityPlugin extends Plugin {
    public function execute(): void {
        echo "[SECURITY] Checking permissions\n";
    }
}

class PluginManager {
    /** @var Plugin[] */
    private array $plugins = [];
    
    public function register(Plugin $plugin): void {
        $this->plugins[] = $plugin;
    }
    
    public function runAll(): void {
        foreach ($this->plugins as $plugin) {
            if ($plugin->isActive()) {
                $plugin->execute();  // Polymorphic call
            }
        }
    }
}

// Usage
$manager = new PluginManager();
$manager->register(new LoggingPlugin());
$manager->register(new CachingPlugin());
$manager->register(new SecurityPlugin());

$manager->runAll();
?>
```

---

## 6. Interfaces

### Definition

**Interface**: A contract that defines a set of methods a class must implement. Interfaces contain only method signatures (no implementation), forcing implementing classes to provide concrete implementations.

**implements**: The keyword used to indicate a class implements an interface.

**Contract**: An agreement that a class will provide specific methods with specific signatures.

**Multiple Interface Implementation**: PHP allows a class to implement multiple interfaces, enabling different types of behavior.

### Interface Implementation Diagram

```
┌──────────────────────────────────────────────────────────────────┐
│                     Interface Contract                           │
└──────────────────────────────────────────────────────────────────┘

┌───────────────────────┐
│ <<interface>>         │
│    LoggerInterface    │
├───────────────────────┤
│ + log(msg, level)     │
│ + error(msg)          │
│ + info(msg)           │
└───────────┬───────────┘
            │ implements
    ┌───────┴───────┐
    │               │
    v               v
┌──────────┐   ┌──────────┐
│FileLogger│   │ Database │
│          │   │  Logger  │
├──────────┤   ├──────────┤
│-filePath │   │  - db    │
├──────────┤   ├──────────┤
│+ log()   │   │+ log()   │
│+ error() │   │+ error() │
│+ info()  │   │+ info()  │
└──────────┘   └──────────┘

Both classes satisfy the LoggerInterface contract
but implement methods differently
```

### Defining Interfaces

**Definition:** An **Interface** defines a contract that a class must adhere to. It specifies *what* methods a class must implement, but not *how*. All methods in an interface must be public and abstract (no body). Interfaces enable polymorphism by allowing different classes to be treated interchangeably based on their shared capabilities.

```php
<?php
// Interface - contract that classes must follow
interface LoggerInterface {
    // Interface methods are abstract and public by default
    public function log(string $message, string $level = 'info'): void;
    public function error(string $message): void;
    public function info(string $message): void;
}

// Implementing interface
class FileLogger implements LoggerInterface {
    private string $filePath;
    
    public function __construct(string $filePath) {
        $this->filePath = $filePath;
    }
    
    public function log(string $message, string $level = 'info'): void {
        $line = "[{$level}] " . date('Y-m-d H:i:s') . " - {$message}\n";
        file_put_contents($this->filePath, $line, FILE_APPEND);
    }
    
    public function error(string $message): void {
        $this->log($message, 'error');
    }
    
    public function info(string $message): void {
        $this->log($message, 'info');
    }
}

class DatabaseLogger implements LoggerInterface {
    public function log(string $message, string $level = 'info'): void {
        // Save to database
        echo "Saving to DB: [{$level}] {$message}\n";
    }
    
    public function error(string $message): void {
        $this->log($message, 'error');
    }
    
    public function info(string $message): void {
        $this->log($message, 'info');
    }
}

// Usage with type hinting
function processOrder(LoggerInterface $logger, array $order): void {
    $logger->info('Processing order #' . $order['id']);
    
    try {
        // Process order...
        $logger->info('Order processed successfully');
    } catch (Exception $e) {
        $logger->error('Order processing failed: ' . $e->getMessage());
    }
}

$fileLogger = new FileLogger('/var/log/app.log');
$dbLogger = new DatabaseLogger();

processOrder($fileLogger, ['id' => 123]);
processOrder($dbLogger, ['id' => 456]);
?>
```

### Multiple Interfaces

**Definition:** While PHP does not support multiple inheritance for classes (extending multiple parents), a class can implement **multiple interfaces** by separating them with commas. This allows a class to fulfill multiple roles (contracts) simultaneously, promoting flexible and decoupled design.

```php
<?php
interface JsonSerializable {
    public function toJson(): string;
}

interface ArraySerializable {
    public function toArray(): array;
}

interface Validatable {
    public function validate(): bool;
    public function getErrors(): array;
}

// Implementing multiple interfaces
class User implements JsonSerializable, ArraySerializable, Validatable {
    private array $errors = [];
    
    public function __construct(
        private string $name,
        private string $email,
        private int $age
    ) {}
    
    public function toJson(): string {
        return json_encode($this->toArray());
    }
    
    public function toArray(): array {
        return [
            'name' => $this->name,
            'email' => $this->email,
            'age' => $this->age
        ];
    }
    
    public function validate(): bool {
        $this->errors = [];
        
        if (empty($this->name)) {
            $this->errors[] = 'Name is required';
        }
        
        if (!filter_var($this->email, FILTER_VALIDATE_EMAIL)) {
            $this->errors[] = 'Invalid email format';
        }
        
        if ($this->age < 18) {
            $this->errors[] = 'Must be 18 or older';
        }
        
        return empty($this->errors);
    }
    
    public function getErrors(): array {
        return $this->errors;
    }
}

$user = new User('John', 'john@example.com', 25);

if ($user->validate()) {
    echo $user->toJson();
} else {
    print_r($user->getErrors());
}
?>
```

### Interface vs Abstract Class

| Feature | Interface | Abstract Class |
|---------|-----------|----------------|
| **Methods** | Only method signatures (PHP 8+ allows default implementations) | Can have both abstract and concrete methods |
| **Properties** | Only constants (no properties) | Can have properties |
| **Multiple** | A class can implement multiple interfaces | A class can extend only one abstract class |
| **Constructor** | Cannot have constructor | Can have constructor |
| **Use Case** | Define a contract/capability | Share code among related classes |

```php
<?php
// Interface - defines capabilities
interface Payable {
    public function pay(float $amount): bool;
    public function refund(float $amount): bool;
}

interface Subscribable {
    public function subscribe(): void;
    public function cancel(): void;
}

// Abstract class - shared implementation
abstract class Customer {
    protected string $id;
    protected string $name;
    protected array $paymentHistory = [];
    
    public function __construct(string $name) {
        $this->id = uniqid('cust_');
        $this->name = $name;
    }
    
    public function getPaymentHistory(): array {
        return $this->paymentHistory;
    }
}

// Concrete class - extends abstract and implements interfaces
class PremiumCustomer extends Customer implements Payable, Subscribable {
    private bool $isSubscribed = false;
    
    public function pay(float $amount): bool {
        $this->paymentHistory[] = ['amount' => $amount, 'date' => new DateTime()];
        return true;
    }
    
    public function refund(float $amount): bool {
        $this->paymentHistory[] = ['amount' => -$amount, 'date' => new DateTime()];
        return true;
    }
    
    public function subscribe(): void {
        $this->isSubscribed = true;
    }
    
    public function cancel(): void {
        $this->isSubscribed = false;
    }
}
?>
```

---

## 7. Traits

### Definition

**Trait**: A mechanism for code reuse in single inheritance languages like PHP. Traits allow developers to reuse sets of methods freely in several independent classes living in different class hierarchies.

**use**: The keyword used to include a trait in a class.

**Conflict Resolution**: When multiple traits define the same method, PHP provides mechanisms to resolve which method to use or alias methods.

**Horizontal Reuse**: Traits enable code reuse across unrelated classes, unlike inheritance which is vertical.

### Trait Composition Diagram

```
┌──────────────────────────────────────────────────────────────────┐
│                     Trait Composition                            │
└──────────────────────────────────────────────────────────────────┘

       ┌─────────────────────┐         ┌─────────────────────┐
       │   Timestampable     │         │    SoftDeletable    │
       │      (trait)        │         │       (trait)       │
       ├─────────────────────┤         ├─────────────────────┤
       │ - createdAt         │         │ - deletedAt         │
       │ - updatedAt         │         ├─────────────────────┤
       ├─────────────────────┤         │ + delete()          │
       │ + getCreatedAt()    │         │ + restore()         │
       │ + getUpdatedAt()    │         │ + isDeleted()       │
       │ + touch()           │         └──────────┬──────────┘
       └──────────┬──────────┘                    │
                  │                               │
                  │         use                   │
                  └──────────┬────────────────────┘
                             │
                             ▼
                ┌──────────────────────┐
                │         Post         │
                │        (class)       │
                ├──────────────────────┤
                │ - title              │
                │ - content            │
                ├──────────────────────┤
                │ + getTitle()         │
                │ + getContent()       │
                └──────────────────────┘
                
                Post includes ALL methods from
                both Timestampable AND SoftDeletable
```

### Defining Traits

**Definition:** A **Trait** is a mechanism for code reuse in single-inheritance languages like PHP. It allows you to define a set of methods that can be included in multiple independent classes (horizontal code reuse). Traits avoid the limitations of class inheritance by enabling composition of behavior.

```php
<?php
// Trait - reusable code that can be included in multiple classes
trait Timestampable {
    private DateTimeImmutable $createdAt;
    private ?DateTimeImmutable $updatedAt = null;
    
    public function initializeTimestamps(): void {
        $this->createdAt = new DateTimeImmutable();
    }
    
    public function getCreatedAt(): DateTimeImmutable {
        return $this->createdAt;
    }
    
    public function getUpdatedAt(): ?DateTimeImmutable {
        return $this->updatedAt;
    }
    
    public function touch(): void {
        $this->updatedAt = new DateTimeImmutable();
    }
}

trait SoftDeletable {
    private ?DateTimeImmutable $deletedAt = null;
    
    public function delete(): void {
        $this->deletedAt = new DateTimeImmutable();
    }
    
    public function restore(): void {
        $this->deletedAt = null;
    }
    
    public function isDeleted(): bool {
        return $this->deletedAt !== null;
    }
}

trait HasLogger {
    private LoggerInterface $logger;
    
    public function setLogger(LoggerInterface $logger): void {
        $this->logger = $logger;
    }
    
    protected function log(string $message, string $level = 'info'): void {
        if (isset($this->logger)) {
            $this->logger->log($message, $level);
        }
    }
}

// Using traits in classes
class Post {
    use Timestampable;
    use SoftDeletable;
    use HasLogger;
    
    public function __construct(private string $title, private string $content) {
        $this->initializeTimestamps();
        $this->log('Post created: ' . $title);
    }
}

class Comment {
    use Timestampable;
    use HasLogger;
    
    public function __construct(private string $content) {
        $this->initializeTimestamps();
    }
}

$post = new Post('Hello World', 'Content here...');
echo $post->getCreatedAt()->format('Y-m-d H:i:s');
$post->delete();
echo $post->isDeleted() ? 'Yes' : 'No';
?>
```

### Conflict Resolution

```php
<?php
trait HasName {
    public function getName(): string {
        return 'Name from HasName';
    }
    
    public function greet(): string {
        return 'Hello from HasName';
    }
}

trait HasTitle {
    public function getName(): string {
        return 'Name from HasTitle';
    }
    
    public function greet(): string {
        return 'Hello from HasTitle';
    }
}

class Product {
    use HasName, HasTitle {
        // Resolve conflict: use HasName's version
        HasName::getName insteadof HasTitle;
        
        // Resolve conflict: use HasTitle's version
        HasTitle::greet insteadof HasName;
        
        // Alias HasTitle's getName to access it with different name
        HasTitle::getName as getTitle;
    }
}

$product = new Product();
echo $product->getName();    // Name from HasName
echo $product->getTitle();   // Name from HasTitle
echo $product->greet();      // Hello from HasTitle
?>
```

### Trait Properties

```php
<?php
trait ConfigTrait {
    // Trait properties cannot have default values if conflicting
    protected array $config = [];
    
    public function setConfig(array $config): void {
        $this->config = array_merge($this->config, $config);
    }
    
    public function getConfig(string $key, mixed $default = null): mixed {
        return $this->config[$key] ?? $default;
    }
}

class Application {
    use ConfigTrait;
    
    // Can override trait property default
    protected array $config = [
        'debug' => false,
        'timezone' => 'UTC'
    ];
    
    public function __construct() {
        $this->setConfig(['version' => '1.0.0']);
    }
}

$app = new Application();
echo $app->getConfig('debug') ? 'Yes' : 'No';  // No
echo $app->getConfig('version');               // 1.0.0
?>
```

### When to Use Traits

**Definition:** Use traits when multiple classes need to share the same implementation logic but do not share a common ancestor (or when inheritance would feel forced). Common use cases include logging, caching, singleton enforcement, or adding utility methods to unrelated classes.
- **Share code** across unrelated classes
- **Avoid deep inheritance** hierarchies
- **Mix in functionality** without breaking single responsibility
- **Horizontal code reuse** instead of vertical (inheritance)

---

## 8. Static Methods & Properties

### Definition

**Static**: Members that belong to the class itself rather than to instances of the class. They can be accessed without creating an object.

**static**: The keyword used to declare static properties and methods.

**self::**: Refers to the class where the method is defined (early binding).

**static::**: Refers to the class that was called (late static binding), allowing for polymorphic behavior with static methods.

**Singleton Pattern**: A design pattern that restricts a class to a single instance, typically implemented using static methods.

### Static Members Diagram

```
┌──────────────────────────────────────────────────────────────────┐
│                     Static Members                               │
│              (Shared Across All Instances)                       │
└──────────────────────────────────────────────────────────────────┘

         Database (Class)
         ┌──────────────────────┐
         │ Static:              │
         │ - $instance = null   │<─────┐
         │ - $count = 0         │      │ Shared by
         │                      │      │ all instances
         │ Static Methods:      │      │
         │ + getInstance()      │      │
         │ + getCount()         │      │
         ├──────────────────────┤      │
         │ Instance:            │      │
         │ - $connection        │      │
         │                      │      │
         │ Instance Methods:    │      │
         │ + query()            │      │
         │ + insert()           │      │
         └──────────────────────┘      │
                   │                   │
        ┌──────────┴──────────┐        │
        │                     │        │
        v                     v        │
   $db1 = new        $db2 = new       │
   Database()        Database()       │
                      │               │
                      └───────────────┘
                      
   Both $db1 and $db2 reference the
   SAME static $instance and $count
```

### Static Keyword

**Definition:** The `static` keyword defines properties or methods that belong to the class itself rather than to any specific instance (object). Static members are accessed using the scope resolution operator `::` (e.g., `ClassName::$property`). They are commonly used for utility functions or global configurations.

```php
<?php
class Database {
    // Static property - shared across all instances
    private static ?self $instance = null;
    private static int $connectionCount = 0;
    
    private PDO $connection;
    
    // Private constructor for singleton
    private function __construct() {
        $this->connection = new PDO('mysql:host=localhost;dbname=test', 'user', 'pass');
        self::$connectionCount++;
    }
    
    // Static method - called on class, not instance
    public static function getInstance(): self {
        if (self::$instance === null) {
            self::$instance = new self();
        }
        return self::$instance;
    }
    
    public static function getConnectionCount(): int {
        return self::$connectionCount;
    }
    
    // Instance method
    public function query(string $sql): array {
        return $this->connection->query($sql)->fetchAll();
    }
}

// Using static methods
$db1 = Database::getInstance();
$db2 = Database::getInstance();

echo ($db1 === $db2) ? 'Same instance' : 'Different instances';  // Same instance
echo Database::getConnectionCount();  // 1
?>
```

### self:: vs static:: (Late Static Binding)

**Definition:** `self::` refers to the class where the code is *written* (early binding). `static::` refers to the class that was *called* at runtime (late static binding). This distinction is crucial in inheritance scenarios where a child class overrides a static method or property — `static::` allows access to the child's version.

```php
<?php
class ParentClass {
    protected static string $name = 'Parent';
    
    public static function getNameSelf(): string {
        // self refers to the class where the method is defined
        return self::$name;
    }
    
    public static function getNameStatic(): string {
        // static refers to the class that was called (late static binding)
        return static::$name;
    }
}

class ChildClass extends ParentClass {
    protected static string $name = 'Child';
}

echo ParentClass::getNameSelf();    // Parent
echo ParentClass::getNameStatic();  // Parent

echo ChildClass::getNameSelf();     // Parent  (self refers to ParentClass)
echo ChildClass::getNameStatic();   // Child   (static refers to ChildClass)
?>
```

### Practical Example: Counter

```php
<?php
class Counter {
    private static int $globalCount = 0;
    private int $instanceCount = 0;
    
    public function increment(): void {
        $this->instanceCount++;
        self::$globalCount++;
    }
    
    public function getInstanceCount(): int {
        return $this->instanceCount;
    }
    
    public static function getGlobalCount(): int {
        return self::$globalCount;
    }
}

$counter1 = new Counter();
$counter2 = new Counter();

$counter1->increment();  // instance=1, global=1
$counter1->increment();  // instance=2, global=2
$counter2->increment();  // instance=1, global=3

echo $counter1->getInstanceCount();  // 2
echo $counter2->getInstanceCount();  // 1
echo Counter::getGlobalCount();      // 3
?>
```

### When to Use Static

**Definition:** Use static methods for utility functions that do not depend on object state (stateless operations) or for specialized factory methods that create instances (`User::create()`). Avoid using static properties for mutable global state, as it makes testing and concurrency difficult.
- **Utility functions** (e.g., `MathHelper::calculate()`)
- **Singleton pattern** (database connections, config)
- **Factory methods** (creating instances)
- **Counters or global state** (use sparingly)

### Avoid
- Static for dependencies (hard to test)
- Static mutable state (can cause bugs)
- Overuse of static (defeats OOP benefits)

---

## 9. Magic Methods

### Definition

**Magic Methods**: Special methods in PHP that start with double underscores (`__`) and are automatically called by PHP in certain situations. They allow objects to behave in specific ways.

**__construct**: Called when an object is created.

**__destruct**: Called when an object is destroyed.

**__get/__set**: Called when accessing/setting inaccessible properties.

**__call**: Called when invoking inaccessible methods.

**__toString**: Called when an object is used as a string.

### Magic Methods Overview

### Magic Methods Reference

| Method | Trigger | Description |
|--------|---------|-------------|
| `__construct()` | Creation | Called when object is created |
| `__destruct()` | Destruction | Called when object is destroyed |
| `__get($name)` | Property Read | Called when reading inaccessible property |
| `__set($name, $val)` | Property Write | Called when writing to inaccessible property |
| `__isset($name)` | Property Check | Called when `isset()` or `empty()` used on property |
| `__unset($name)` | Property Unset | Called when `unset()` used on property |
| `__call($n, $args)` | Method Call | Called when invoking inaccessible method |
| `__toString()` | String Conversion | Called when object is treated as a string |
| `__invoke()` | Function Call | Called when object is called as a function |
| `__clone()` | Cloning | Called when object is cloned |

  │    __call    │        │  __toString  │        │   __invoke   │
  │(call method) │        │ (as string)  │        │(as function) │
  └──────────────┘        └──────────────┘        └──────────────┘
  
  ┌──────────────┐        ┌──────────────┐
  │   __clone    │        │__sleep/wakeup│
  │  (duplicate) │        │(serialize)   │
  └──────────────┘        └──────────────┘
```

### Common Magic Methods

```php
<?php
class MagicDemo {
    // Properties
    private array $data = [];
    private string $name;
    
    // 1. __construct - called when object is created
    public function __construct(string $name) {
        echo "Constructor called\n";
        $this->name = $name;
    }
    
    // 2. __destruct - called when object is destroyed
    public function __destruct() {
        echo "Destructor called for {$this->name}\n";
    }
    
    // 3. __get - called when accessing undefined/inaccessible property
    public function __get(string $name): mixed {
        echo "Getting {$name}\n";
        return $this->data[$name] ?? null;
    }
    
    // 4. __set - called when setting undefined/inaccessible property
    public function __set(string $name, mixed $value): void {
        echo "Setting {$name} = {$value}\n";
        $this->data[$name] = $value;
    }
    
    // 5. __isset - called when using isset() or empty()
    public function __isset(string $name): bool {
        echo "Checking if {$name} is set\n";
        return isset($this->data[$name]);
    }
    
    // 6. __unset - called when using unset()
    public function __unset(string $name): void {
        echo "Unsetting {$name}\n";
        unset($this->data[$name]);
    }
    
    // 7. __call - called when invoking undefined/inaccessible method
    public function __call(string $name, array $arguments): mixed {
        echo "Calling method {$name} with arguments: " . implode(', ', $arguments) . "\n";
        return "Result from {$name}";
    }
    
    // 8. __toString - called when object is used as string
    public function __toString(): string {
        return "MagicDemo: {$this->name}";
    }
    
    // 9. __invoke - called when object is called as function
    public function __invoke(string $message): string {
        return "Invoked with: {$message}";
    }
    
    // 10. __clone - called when object is cloned
    public function __clone() {
        echo "Cloning {$this->name}\n";
        $this->name = $this->name . ' (clone)';
    }
}

// Usage
$obj = new MagicDemo('Test');      // Constructor called

// __get and __set
$obj->email = 'test@example.com';  // Setting email = test@example.com
echo $obj->email;                  // Getting email -> test@example.com

// __isset and __unset
isset($obj->email);                // Checking if email is set
unset($obj->email);                // Unsetting email

// __call
echo $obj->doSomething('arg1', 'arg2');  // Calling method doSomething...

// __toString
echo $obj;                         // MagicDemo: Test

// __invoke
echo $obj('Hello!');               // Invoked with: Hello!

// __clone
$clone = clone $obj;               // Cloning Test

unset($obj);                       // Destructor called for Test
unset($clone);                     // Destructor called for Test (clone)
?>
```

### Practical Example: Array-like Object

```php
<?php
class Collection implements ArrayAccess, Countable, Iterator {
    private array $items = [];
    private int $position = 0;
    
    public function __construct(array $items = []) {
        $this->items = $items;
    }
    
    // ArrayAccess implementation
    public function offsetExists($offset): bool {
        return isset($this->items[$offset]);
    }
    
    public function offsetGet($offset): mixed {
        return $this->items[$offset] ?? null;
    }
    
    public function offsetSet($offset, $value): void {
        if ($offset === null) {
            $this->items[] = $value;
        } else {
            $this->items[$offset] = $value;
        }
    }
    
    public function offsetUnset($offset): void {
        unset($this->items[$offset]);
    }
    
    // Countable implementation
    public function count(): int {
        return count($this->items);
    }
    
    // Iterator implementation
    public function rewind(): void {
        $this->position = 0;
    }
    
    public function current(): mixed {
        return $this->items[array_keys($this->items)[$this->position]];
    }
    
    public function key(): mixed {
        return array_keys($this->items)[$this->position];
    }
    
    public function next(): void {
        $this->position++;
    }
    
    public function valid(): bool {
        return $this->position < count($this->items);
    }
    
    // __toString
    public function __toString(): string {
        return json_encode($this->items);
    }
}

$collection = new Collection(['apple', 'banana', 'cherry']);

// Use as array
echo $collection[0];           // apple
$collection[] = 'date';        // Add item
echo count($collection);       // 4

// Iterate
foreach ($collection as $key => $value) {
    echo "{$key}: {$value}\n";
}

// Convert to string
echo $collection;              // ["apple","banana","cherry","date"]
?>
```

### Serialization Magic Methods

```php
<?php
class UserSession {
    private int $userId;
    private string $username;
    private DateTimeImmutable $loginTime;
    private string $sensitiveData;  // Should not be serialized
    
    public function __construct(int $userId, string $username) {
        $this->userId = $userId;
        $this->username = $username;
        $this->loginTime = new DateTimeImmutable();
        $this->sensitiveData = 'secret-token';
    }
    
    // Called before serialization
    public function __sleep(): array {
        // Only serialize these properties
        return ['userId', 'username', 'loginTime'];
    }
    
    // Called after unserialization
    public function __wakeup(): void {
        // Restore sensitive data
        $this->sensitiveData = 'restored-token';
        echo "Session restored for {$this->username}\n";
    }
    
    // Alternative: __serialize (PHP 7.4+)
    public function __serialize(): array {
        return [
            'userId' => $this->userId,
            'username' => $this->username,
            'loginTime' => $this->loginTime->format('c')
        ];
    }
    
    // Alternative: __unserialize (PHP 7.4+)
    public function __unserialize(array $data): void {
        $this->userId = $data['userId'];
        $this->username = $data['username'];
        $this->loginTime = new DateTimeImmutable($data['loginTime']);
        $this->sensitiveData = 'restored';
    }
}

$session = new UserSession(123, 'john_doe');
$serialized = serialize($session);
$restored = unserialize($serialized);
?>
```

---

## 10. Namespaces & Autoloading

### Definition

**Namespace**: A way to encapsulate classes, interfaces, functions, and constants to avoid naming collisions and organize code hierarchically.

**Autoloading**: The automatic loading of class files when they are first referenced, eliminating the need for manual require/include statements.

**PSR-4**: A PHP standard for autoloading classes from file paths based on their namespace.

**use**: The keyword to import classes from other namespaces.

**Composer**: A dependency manager for PHP that provides PSR-4 autoloading.

### Namespace Structure Diagram

```
┌──────────────────────────────────────────────────────────────────┐
│                  Namespace Hierarchy                             │
└──────────────────────────────────────────────────────────────────┘

                    App (Root Namespace)
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        v                v                v
    ┌────────┐      ┌──────────┐     ┌──────────┐
    │Models  │      │Controllers│    │ Services │
    ├────────┤      ├───────────┤    ├──────────┤
    │User.php│      │UserCtrl   │    │EmailSvc  │
    │Post.php│      │PostCtrl   │    │CacheSvc  │
    │...     │      │...        │    │...       │
    └────────┘      └───────────┘    └───────────┘

File Structure:
src/
├── Models/
│   ├── User.php      (namespace App\Models)
│   └── Post.php      (namespace App\Models)
├── Controllers/
│   ├── UserController.php  (namespace App\Controllers)
│   └── PostController.php  (namespace App\Controllers)
└── Services/
    ├── EmailService.php    (namespace App\Services)
    └── CacheService.php    (namespace App\Services)
```

### namespace Keyword

```php
<?php
// File: src/Models/User.php
namespace App\Models;

class User {
    private int $id;
    private string $name;
    
    public function __construct(int $id, string $name) {
        $this->id = $id;
        $this->name = $name;
    }
}
?>
```

```php
<?php
// File: src/Controllers/UserController.php
namespace App\Controllers;

// Import classes from other namespaces
use App\Models\User;
use DateTimeImmutable;

class UserController {
    public function show(int $id): User {
        return new User($id, 'John Doe');
    }
    
    public function getCurrentTime(): DateTimeImmutable {
        return new DateTimeImmutable();
    }
}
?>
```

```php
<?php
// File: public/index.php
namespace App;

require_once __DIR__ . '/../vendor/autoload.php';

// Fully qualified name
$user = new \App\Models\User(1, 'Jane');

// Or with use statement
use App\Models\User;
use App\Controllers\UserController;

$controller = new UserController();
$user = $controller->show(1);

// Alias
use App\Models\User as UserModel;
$user = new UserModel(2, 'Bob');
?>
```

### PSR-4 Autoloading

**Definition:** PSR-4 is the standard PHP recommendation for autoloading classes from file paths. It maps a namespace prefix (e.g., `App\`) to a base directory (e.g., `src/`). When a class like `App\Models\User` is instantiated, the autoloader knows to look for the file `src/Models/User.php`. This eliminates manual `require` statements.

```json
// composer.json
{
    "name": "myapp/myproject",
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    }
}
```

```
Directory Structure:
project/
├── composer.json
├── vendor/
│   └── autoload.php
└── src/
    ├── Models/
    │   └── User.php      (namespace App\Models)
    ├── Controllers/
    │   └── UserController.php  (namespace App\Controllers)
    └── Services/
        └── EmailService.php    (namespace App\Services)
```

```php
<?php
// After running: composer dump-autoload

require_once __DIR__ . '/vendor/autoload.php';

// Classes are automatically loaded
use App\Models\User;
use App\Controllers\UserController;
use App\Services\EmailService;

$user = new User(1, 'John');
$controller = new UserController();
$emailService = new EmailService();
?>
```

### Custom Autoloader

```php
<?php
// Custom autoloader (understanding how it works)
spl_autoload_register(function (string $class): void {
    // Convert namespace separators to directory separators
    $path = str_replace('\\', DIRECTORY_SEPARATOR, $class);
    
    // Base directory
    $baseDir = __DIR__ . '/src/';
    
    // Full file path
    $file = $baseDir . $path . '.php';
    
    if (file_exists($file)) {
        require_once $file;
    }
});

// Now this will automatically load src/App/Models/User.php
$user = new \App\Models\User(1, 'John');
?>
```

### Best Practices
- Always declare namespace at the top of the file
- Use `use` statements for cleaner code
- Follow PSR-4 naming conventions
- Use Composer for autoloading in production
- Organize namespaces by functionality (Models, Controllers, Services)

---

## 11. Dependency Injection

### Definition

**Dependency Injection (DI)**: A design pattern where dependencies (objects a class needs) are provided from the outside rather than created internally. This promotes loose coupling and makes code more testable.

**Inversion of Control (IoC)**: The principle that controls the flow of a program is inverted - instead of objects creating their dependencies, dependencies are injected into objects.

**Constructor Injection**: The preferred method of DI where dependencies are passed through the constructor.

**Interface/Type Hinting**: Using interfaces as type hints to allow any implementation of that interface to be injected.

**Service Container**: A tool that manages object creation and dependency resolution automatically.

### Dependency Injection Pattern Diagram

```
┌──────────────────────────────────────────────────────────────────┐
│               Dependency Injection Pattern                       │
│                    (Loose Coupling)                              │
└──────────────────────────────────────────────────────────────────┘

WITHOUT DI (Tight Coupling):
┌──────────────────────┐
│    OrderService      │
├──────────────────────┤
│ - db: MySQLDatabase  │  <-- Hard-coded dependency
│ - log: FileLogger    │      (created internally)
├──────────────────────┤
│ + createOrder()      │
└──────────────────────┘
        X
   Cannot easily swap
   implementations

WITH DI (Loose Coupling):
┌──────────────────────────────────────────────────────┐
│                    OrderService                       │
├──────────────────────────────────────────────────────┤
│ - db: DatabaseInterface  <-- Injected from outside   │
│ - log: LoggerInterface                                 │
├──────────────────────────────────────────────────────┤
│ + __construct(db, logger)                            │
│ + createOrder()                                      │
└──────────────────────────────────────────────────────┘
         ^
         | can use any
    ┌────┴────┐
    │         │
    v         v
┌────────┐  ┌──────────────┐  ┌──────────────┐
│MySQLDb │  │PostgreSQLDb  │  │ SQLiteDb     │
└────────┘  └──────────────┘  └──────────────┘

Can inject mock objects for testing!
```

### What is DI

**Definition:** Dependency Injection (DI) is a design pattern where a class receives its dependencies (objects it needs) from an external source rather than creating them itself. This promotes loose coupling, making code easier to test and maintain because dependencies can be swapped or mocked.

```php
<?php
// WITHOUT Dependency Injection - tight coupling
class OrderService {
    private Database $db;
    private Logger $logger;
    
    public function __construct() {
        // Hard-coded dependencies - difficult to test and change
        $this->db = new Database('localhost', 'user', 'pass');
        $this->logger = new FileLogger('/var/log/app.log');
    }
}

// WITH Dependency Injection - loose coupling
class OrderServiceDI {
    public function __construct(
        private DatabaseInterface $db,
        private LoggerInterface $logger
    ) {}
    
    public function createOrder(array $data): Order {
        $this->logger->info('Creating order...');
        // Use injected dependencies
        return $this->db->insert('orders', $data);
    }
}

// Inject dependencies from outside
$db = new MySQLDatabase('localhost', 'user', 'pass');
$logger = new FileLogger('/var/log/app.log');
$orderService = new OrderServiceDI($db, $logger);

// Easy to swap implementations for testing
$mockDb = new MockDatabase();
$mockLogger = new MockLogger();
$testService = new OrderServiceDI($mockDb, $mockLogger);
?>
```

### Constructor Injection (Preferred)

**Definition:** Constructor injection passes dependencies through the class constructor. This is the preferred method because it ensures the class is fully initialized with all required dependencies before use, making the object's state valid and predictable from the start.

```php
<?php
interface MailerInterface {
    public function send(string $to, string $subject, string $body): bool;
}

class SmtpMailer implements MailerInterface {
    public function __construct(
        private string $host,
        private string $username,
        private string $password
    ) {}
    
    public function send(string $to, string $subject, string $body): bool {
        // SMTP implementation
        return true;
    }
}

class SendGridMailer implements MailerInterface {
    public function __construct(private string $apiKey) {}
    
    public function send(string $to, string $subject, string $body): bool {
        // SendGrid API implementation
        return true;
    }
}

class NotificationService {
    public function __construct(
        private MailerInterface $mailer,  // Depends on abstraction
        private LoggerInterface $logger
    ) {}
    
    public function notifyUser(User $user, string $message): void {
        $this->logger->info("Notifying user: {$user->getEmail()}");
        
        $this->mailer->send(
            $user->getEmail(),
            'Notification',
            $message
        );
    }
}

// Usage - easy to swap mailer implementations
$smtpMailer = new SmtpMailer('smtp.example.com', 'user', 'pass');
$notificationService = new NotificationService($smtpMailer, $logger);

// Or use SendGrid
$sendGridMailer = new SendGridMailer('api-key-here');
$notificationService = new NotificationService($sendGridMailer, $logger);
?>
```

### Interface-Based Injection

**Definition:** Interface-based injection involves type-hinting an interface in the constructor rather than a concrete class. This adheres to the Dependency Inversion Principle, allowing you to swap implementations (e.g., `FileLogger` vs `DbLogger`) without modifying the dependent class.

```php
<?php
// Define contracts
interface CacheInterface {
    public function get(string $key): ?array;
    public function set(string $key, array $value, int $ttl = 3600): void;
    public function delete(string $key): void;
}

interface RepositoryInterface {
    public function find(int $id): ?object;
    public function findAll(): array;
}

// Implementations
class RedisCache implements CacheInterface {
    private Redis $redis;
    
    public function __construct(Redis $redis) {
        $this->redis = $redis;
    }
    
    public function get(string $key): ?array {
        $data = $this->redis->get($key);
        return $data ? json_decode($data, true) : null;
    }
    
    public function set(string $key, array $value, int $ttl = 3600): void {
        $this->redis->setex($key, $ttl, json_encode($value));
    }
    
    public function delete(string $key): void {
        $this->redis->del($key);
    }
}

class FileCache implements CacheInterface {
    private string $cacheDir;
    
    public function __construct(string $cacheDir) {
        $this->cacheDir = $cacheDir;
    }
    
    public function get(string $key): ?array {
        $file = $this->cacheDir . '/' . $key . '.cache';
        if (!file_exists($file)) return null;
        
        $data = unserialize(file_get_contents($file));
        if ($data['expires'] < time()) {
            unlink($file);
            return null;
        }
        return $data['value'];
    }
    
    public function set(string $key, array $value, int $ttl = 3600): void {
        $file = $this->cacheDir . '/' . $key . '.cache';
        file_put_contents($file, serialize([
            'expires' => time() + $ttl,
            'value' => $value
        ]));
    }
    
    public function delete(string $key): void {
        $file = $this->cacheDir . '/' . $key . '.cache';
        if (file_exists($file)) unlink($file);
    }
}

// Cached repository using DI
class CachedUserRepository implements RepositoryInterface {
    public function __construct(
        private RepositoryInterface $repository,  // Decorated repository
        private CacheInterface $cache,
        private int $cacheTtl = 3600
    ) {}
    
    public function find(int $id): ?object {
        $cacheKey = "user_{$id}";
        
        // Try cache first
        if ($cached = $this->cache->get($cacheKey)) {
            return (object) $cached;
        }
        
        // Fetch from repository
        $user = $this->repository->find($id);
        
        if ($user) {
            $this->cache->set($cacheKey, (array) $user, $this->cacheTtl);
        }
        
        return $user;
    }
    
    public function findAll(): array {
        return $this->repository->findAll();
    }
}

// Composition - combine different implementations
$dbRepo = new DatabaseUserRepository($pdo);
$redisCache = new RedisCache($redis);
$cachedRepo = new CachedUserRepository($dbRepo, $redisCache);

// Or use file cache
$fileCache = new FileCache('/tmp/cache');
$cachedRepo2 = new CachedUserRepository($dbRepo, $fileCache);
?>
```

### Composition Over Inheritance

```php
<?php
// BAD: Inheritance hierarchy
class BaseController {}
class ApiController extends BaseController {}
class UserApiController extends ApiController {}

// GOOD: Composition with DI
class Controller {
    public function __construct(
        protected Request $request,
        protected Response $response,
        protected LoggerInterface $logger
    ) {}
}

class UserController {
    public function __construct(
        private UserRepository $users,
        private ValidatorInterface $validator,
        private EventDispatcher $events
    ) {}
    
    public function create(Request $request): Response {
        // Validate
        $data = $request->getBody();
        if (!$this->validator->validate($data, User::rules())) {
            return new Response(400, ['errors' => $this->validator->errors()]);
        }
        
        // Create user
        $user = $this->users->create($data);
        
        // Dispatch event
        $this->events->dispatch(new UserCreatedEvent($user));
        
        return new Response(201, ['user' => $user]);
    }
}

// Build controller with specific dependencies
$controller = new UserController(
    new EloquentUserRepository(),
    new LaravelValidator(),
    new SymfonyEventDispatcher()
);
?>
```

---

## 12. Design Patterns

### Definition

**Design Patterns**: Reusable solutions to common problems in software design. They provide proven approaches to solving specific architectural challenges.

**Singleton**: Ensures a class has only one instance and provides global access to it.

**Factory**: Creates objects without specifying the exact class to create, allowing for flexibility in object creation.

**MVC (Model-View-Controller)**: Separates application logic into three interconnected components for better organization.

**Repository**: Abstracts data access logic from business logic.

**Decorator**: Adds behavior to objects dynamically without affecting other objects.

### Singleton Pattern

**Definition:** The Singleton pattern ensures a class has only one instance and provides a global point of access to it. It typically involves a private constructor, a static instance property, and a static `getInstance()` method. While useful for things like database connections, it introduces global state (hard to test) and is often considered an anti-pattern.

```
┌──────────────────────────────────────────────────────────────────┐
│                     Singleton Pattern                            │
│                 (Single Instance Control)                        │
└──────────────────────────────────────────────────────────────────┘

         DatabaseConnection (Class)
         ┌──────────────────────────────────────┐
         │ Static:                              │
         │ - $instance: self = null             │
         │                                      │
         │ Private:                             │
         │ - __construct()                      │
         │ - __clone()                          │
         │ - __wakeup()                         │
         │                                      │
         │ Public:                              │
         │ + getInstance(): self                │◄──┐
         │ + getPdo(): PDO                      │   │
         └──────────────────────────────────────┘   │
                      │                             │
                      │ returns                     │ same
                      v                             │ instance
            ┌──────────────────────┐                │
            │   $instance (PDO)    │────────────────┘
            └──────────────────────┘
            
All calls to getInstance() return the same object
```

```php
<?php
// Singleton - ensures only one instance exists
final class DatabaseConnection {
    private static ?self $instance = null;
    private PDO $pdo;
    
    // Prevent instantiation from outside
    private function __construct() {
        $this->pdo = new PDO(
            'mysql:host=localhost;dbname=myapp',
            'username',
            'password',
            [PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION]
        );
    }
    
    // Prevent cloning
    private function __clone() {}
    
    // Prevent unserialization
    public function __wakeup() {
        throw new \Exception("Cannot unserialize singleton");
    }
    
    // Get the single instance
    public static function getInstance(): self {
        if (self::$instance === null) {
            self::$instance = new self();
        }
        return self::$instance;
    }
    
    public function getPdo(): PDO {
        return $this->pdo;
    }
}

// Usage
$db1 = DatabaseConnection::getInstance();
$db2 = DatabaseConnection::getInstance();

var_dump($db1 === $db2);  // true - same instance
?>
```

### Factory Pattern

**Definition:** The Factory pattern provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created. It encapsulates object creation logic, decoupling the client code from the specific classes being instantiated.

```
┌──────────────────────────────────────────────────────────────────┐
│                     Factory Pattern                              │
│              (Object Creation without Exposure)                  │
└──────────────────────────────────────────────────────────────────┘

         NotificationFactory
         ┌────────────────────────────┐
         │ + create(type): Notification│
         │ + createForUser(user, pref) │
         └─────────────┬──────────────┘
                       │ creates
        ┌──────────────┼──────────────┐
        │              │              │
        v              v              v
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│EmailNotification│ SmsNotification│ PushNotification│
├──────────────┤ ├──────────────┤ ├──────────────┤
│+ send()      │ │+ send()      │ │+ send()      │
│+ getChannel()│ │+ getChannel()│ │+ getChannel()│
└──────────────┘ └──────────────┘ └──────────────┘
        │              │              │
        └──────────────┼──────────────┘
                       │
                       v
               Notification (Interface)
               + send(message): void
               + getChannel(): string
```

```php
<?php
// Product interface
interface Notification {
    public function send(string $message): void;
    public function getChannel(): string;
}

// Concrete products
class EmailNotification implements Notification {
    public function send(string $message): void {
        echo "Sending email: {$message}\n";
    }
    
    public function getChannel(): string {
        return 'email';
    }
}

class SmsNotification implements Notification {
    public function send(string $message): void {
        echo "Sending SMS: {$message}\n";
    }
    
    public function getChannel(): string {
        return 'sms';
    }
}

class PushNotification implements Notification {
    public function send(string $message): void {
        echo "Sending push notification: {$message}\n";
    }
    
    public function getChannel(): string {
        return 'push';
    }
}

// Factory
class NotificationFactory {
    public static function create(string $type): Notification {
        return match($type) {
            'email' => new EmailNotification(),
            'sms' => new SmsNotification(),
            'push' => new PushNotification(),
            default => throw new \InvalidArgumentException("Unknown notification type: {$type}")
        };
    }
    
    public static function createForUser(User $user, string $preferredChannel): Notification {
        $channel = $preferredChannel ?? $user->getPreferredChannel() ?? 'email';
        return self::create($channel);
    }
}

// Usage
$notification = NotificationFactory::create('email');
$notification->send('Hello!');

// Factory with logic
$user = new User('john@example.com', 'sms');
$notification = NotificationFactory::createForUser($user, null);
$notification->send('Your order is ready!');
?>
```

### MVC Overview

```
┌──────────────────────────────────────────────────────────────────┐
│                     MVC Pattern                                  │
│          (Model-View-Controller Separation)                      │
└──────────────────────────────────────────────────────────────────┘

     User Request
          │
          v
┌─────────────────────┐
│    Controller       │◄─────── Handles user input, coordinates
├─────────────────────┤         Model and View
│ - model: Model      │
│ - view: View        │
├─────────────────────┤
│ + index()           │
│ + show(id)          │
│ + create(data)      │
└───────┬─────────────┘
        │
   ┌────┴────┐
   │         │
   v         v
┌──────────────┐    ┌──────────────────┐
│    Model     │    │      View        │
│   (Data)     │    │  (Presentation)  │
├──────────────┤    ├──────────────────┤
│ - db: PDO    │    │ - template: string│
├──────────────┤    ├──────────────────┤
│ + find(id)   │    │ + render(data)   │
│ + findAll()  │    │ + renderList()   │
│ + create()   │    │ - escape()       │
│ + update()   │    └──────────────────┘
│ + delete()   │            │
└──────────────┘            │
        │                   │
        └─────────┬─────────┘
                  │
                  v
            Response to User

Separation of Concerns:
- Model: Data and business logic
- View: Presentation layer
- Controller: Coordination and routing
```

```php
<?php
// Model - handles data and business logic
class PostModel {
    private PDO $db;
    
    public function __construct(PDO $db) {
        $this->db = $db;
    }
    
    public function find(int $id): ?array {
        $stmt = $this->db->prepare('SELECT * FROM posts WHERE id = ?');
        $stmt->execute([$id]);
        return $stmt->fetch() ?: null;
    }
    
    public function create(array $data): int {
        $stmt = $this->db->prepare('INSERT INTO posts (title, content, author_id) VALUES (?, ?, ?)');
        $stmt->execute([$data['title'], $data['content'], $data['author_id']]);
        return (int) $this->db->lastInsertId();
    }
}

// View - handles presentation
class PostView {
    public function render(array $post): string {
        return <<<HTML
        <article>
            <h1>{$this->escape($post['title'])}</h1>
            <div class="content">{$this->escape($post['content'])}</div>
            <time>{$post['created_at']}</time>
        </article>
        HTML;
    }
    
    public function renderList(array $posts): string {
        $html = '<div class="posts">';
        foreach ($posts as $post) {
            $html .= $this->render($post);
        }
        return $html . '</div>';
    }
    
    private function escape(string $text): string {
        return htmlspecialchars($text, ENT_QUOTES, 'UTF-8');
    }
}

// Controller - handles requests and coordinates Model/View
class PostController {
    public function __construct(
        private PostModel $model,
        private PostView $view
    ) {}
    
    public function show(int $id): string {
        $post = $this->model->find($id);
        
        if (!$post) {
            http_response_code(404);
            return 'Post not found';
        }
        
        return $this->view->render($post);
    }
    
    public function create(Request $request): string {
        $data = $request->getBody();
        
        // Validation
        if (empty($data['title']) || empty($data['content'])) {
            http_response_code(400);
            return 'Title and content are required';
        }
        
        $postId = $this->model->create($data);
        
        http_response_code(201);
        return "Post created with ID: {$postId}";
    }
}

// Routing (simplified)
$router = new Router();
$router->get('/posts/{id}', [PostController::class, 'show']);
$router->post('/posts', [PostController::class, 'create']);
?>
```

---

## 13. SOLID Principles

### Definition

**SOLID**: An acronym for five design principles intended to make software designs more understandable, flexible, and maintainable.

**S - Single Responsibility Principle (SRP)**: A class should have one, and only one, reason to change.

**O - Open/Closed Principle (OCP)**: Software entities should be open for extension but closed for modification.

**L - Liskov Substitution Principle (LSP)**: Objects of a superclass should be replaceable with objects of subclasses without affecting correctness.

**I - Interface Segregation Principle (ISP)**: Clients should not be forced to depend on interfaces they do not use.

**D - Dependency Inversion Principle (DIP)**: High-level modules should not depend on low-level modules; both should depend on abstractions.

### Single Responsibility Principle (SRP)

**Definition:** The Single Responsibility Principle states that a class should have one, and only one, reason to change. This means a class should encapsulate a single functionality (e.g., distinct logic for saving directly to DB vs formatting output), making it more robust and easier to understand.

```
┌──────────────────────────────────────────────────────────────────┐
│           Single Responsibility Principle                        │
│              (One Reason to Change)                              │
└──────────────────────────────────────────────────────────────────┘

BEFORE (Multiple Responsibilities):
┌─────────────────────────────────────────────┐
│           UserManager                       │
│  X Too many responsibilities                │
├─────────────────────────────────────────────┤
│ + createUser(data)                          │
│ + deleteUser(id)                            │
│ + sendWelcomeEmail(user)     ◄── Email      │
│ + logActivity(action)        ◄── Logging    │
│ + validateInput(data)        ◄── Validation │
└─────────────────────────────────────────────┘

AFTER (Single Responsibility):
         UserRepository
         ┌──────────────────┐
         │ + create(data)   │
         │ + delete(id)     │
         │ + find(id)       │
         └────────┬─────────┘
                  │ manages
                  v
            User Data

         EmailService       UserValidator      ActivityLogger
         ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
         │+ sendWelcome │   │+ validate()  │   │+ log()       │
         └──────────────┘   └──────────────┘   └──────────────┘

Each class has ONE specific responsibility
```

```php
<?php
// BAD: Multiple responsibilities
class UserManager {
    public function createUser($data) { /* ... */ }
    public function deleteUser($id) { /* ... */ }
    public function sendWelcomeEmail($user) { /* ... */ }  // Not user's responsibility
    public function logActivity($action) { /* ... */ }      // Not user's responsibility
    public function validateInput($data) { /* ... */ }      // Not user's responsibility
}

// GOOD: Each class has one responsibility
class UserRepository {
    public function create(array $data): User { /* ... */ }
    public function delete(int $id): bool { /* ... */ }
    public function find(int $id): ?User { /* ... */ }
}

class UserValidator {
    public function validate(array $data): ValidationResult { /* ... */ }
}

class EmailService {
    public function sendWelcomeEmail(User $user): void { /* ... */ }
}

class ActivityLogger {
    public function log(string $action, array $context): void { /* ... */ }
}

// Orchestrated by a service
class UserService {
    public function __construct(
        private UserRepository $users,
        private UserValidator $validator,
        private EmailService $email,
        private ActivityLogger $logger
    ) {}
    
    public function register(array $data): User {
        $validation = $this->validator->validate($data);
        if (!$validation->isValid()) {
            throw new ValidationException($validation->errors());
        }
        
        $user = $this->users->create($data);
        $this->email->sendWelcomeEmail($user);
        $this->logger->log('user_registered', ['user_id' => $user->getId()]);
        
        return $user;
    }
}
?>
```

### Open/Closed Principle (OCP)

**Definition:** The Open/Closed Principle states that software entities (classes, modules, functions) should be open for extension but closed for modification. You should be able to add new functionality (extension) without changing existing code (modification), usually achieved through inheritance or interfaces.

```
┌──────────────────────────────────────────────────────────────────┐
│           Open/Closed Principle                                  │
│     (Open for Extension, Closed for Modification)                │
└──────────────────────────────────────────────────────────────────┘

BEFORE (Must modify to add shapes):
┌─────────────────────────────────────────┐
│         AreaCalculator                  │
│  X Adding new shapes requires           │
│    modifying this class                 │
├─────────────────────────────────────────┤
│ + calculate(shapes):                    │
│   if Rectangle: w*h                     │
│   if Circle: PI*r^2                     │
│   if Triangle: 0.5*b*h   ◄── ADD HERE   │
└─────────────────────────────────────────┘

AFTER (Extend without modifying):
         Shape (Interface)
         ┌──────────────┐
         │ + area()     │
         └──────┬───────┘
                │
     ┌──────────┼──────────┐
     │          │          │
     v          v          v
┌─────────┐ ┌─────────┐ ┌─────────┐
│Rectangle│ │ Circle  │ │ Triangle│  ◄── Can add
│  w*h    │ │ PI*r^2  │ │0.5*b*h  │     new shapes
└─────────┘ └─────────┘ └─────────┘     without changing
                                        existing code

         AreaCalculator
         ┌──────────────────┐
         │ + calculate()    │◄── Loop through shapes
         │   sum all areas  │    and call area()
         └──────────────────┘
```

```php
<?php
// BAD: Must modify existing code to add new shapes
class AreaCalculator {
    public function calculate($shapes) {
        $area = 0;
        foreach ($shapes as $shape) {
            if ($shape instanceof Rectangle) {
                $area += $shape->width * $shape->height;
            } elseif ($shape instanceof Circle) {
                $area += pi() * $shape->radius ** 2;
            }
            // Must add elseif for each new shape!
        }
        return $area;
    }
}

// GOOD: Open for extension, closed for modification
interface Shape {
    public function area(): float;
}

class Rectangle implements Shape {
    public function __construct(private float $width, private float $height) {}
    
    public function area(): float {
        return $this->width * $this->height;
    }
}

class Circle implements Shape {
    public function __construct(private float $radius) {}
    
    public function area(): float {
        return pi() * $this->radius ** 2;
    }
}

// New shape - no changes to existing code needed
class Triangle implements Shape {
    public function __construct(private float $base, private float $height) {}
    
    public function area(): float {
        return 0.5 * $this->base * $this->height;
    }
}

class AreaCalculator {
    /** @param Shape[] $shapes */
    public function calculate(array $shapes): float {
        return array_reduce($shapes, fn($area, $shape) => $area + $shape->area(), 0);
    }
}

// Usage
$calculator = new AreaCalculator();
$area = $calculator->calculate([
    new Rectangle(10, 5),
    new Circle(7),
    new Triangle(10, 5)  // Works without modifying calculator!
]);
?>
```

### Liskov Substitution Principle (LSP)

**Definition:** The Liskov Substitution Principle states that objects of a superclass should be replaceable with objects of its subclasses without breaking the application. Subclasses must uphold the behavior and contracts defined by the parent class (e.g., return types, exceptions thrown).

```
┌──────────────────────────────────────────────────────────────────┐
│           Liskov Substitution Principle                          │
│      (Subtypes must be substitutable for base types)             │
└──────────────────────────────────────────────────────────────────┘

BEFORE (Violation):
┌─────────────────────────────────────────┐
│            Bird                         │
├─────────────────────────────────────────┤
│ + fly()                                 │
└───────────────┬─────────────────────────┘
                │ extends
                v
         ┌──────────────┐
         │   Penguin    │  X VIOLATION!
         ├──────────────┤
         │ + fly()      │     Penguins can't fly
         │   throws     │     but must implement
         │   Exception  │
         └──────────────┘

AFTER (Correct Hierarchy):
         Bird
         ┌──────────────────┐
         │ + eat()          │
         └────────┬─────────┘
                  │ extends
      ┌───────────┴───────────┐
      │                       │
      v                       v
┌──────────────┐      ┌──────────────┐
│  Flyable     │      │   Penguin    │
│  (Interface) │      ├──────────────┤
├──────────────┤      │ + swim()     │
│ + fly()      │      └──────────────┘
└──────┬───────┘
       │ implements
       v
┌──────────────┐
│   Sparrow    │
├──────────────┤
│ + fly()      │
│ + eat()      │
└──────────────┘

Subtypes fulfill the same contract as parent types
```

```php
<?php
// BAD: Subclass violates parent's contract
class Bird {
    public function fly(): void {
        // Fly implementation
    }
}

class Penguin extends Bird {
    public function fly(): void {
        throw new \Exception("Penguins can't fly!");  // Violates LSP
    }
}

// GOOD: Proper inheritance hierarchy
interface Flyable {
    public function fly(): void;
}

class Bird {
    protected string $name;
    
    public function eat(): void { /* ... */ }
}

class Sparrow extends Bird implements Flyable {
    public function fly(): void {
        echo "Flying...\n";
    }
}

class Penguin extends Bird {
    // Penguins are birds but don't implement Flyable
    public function swim(): void {
        echo "Swimming...\n";
    }
}

// Functions expecting Flyable will work correctly
function makeItFly(Flyable $bird): void {
    $bird->fly();  // Always works - LSP respected
}

makeItFly(new Sparrow());  // OK
// makeItFly(new Penguin());  // Type error - caught at compile time
?>
```

### Interface Segregation Principle (ISP)

**Definition:** The Interface Segregation Principle states that no client should be forced to depend on methods it does not use. Instead of one "fat" interface containing many methods, split it into smaller, more specific interfaces so implementing classes only need to define relevant behavior.

```
┌──────────────────────────────────────────────────────────────────┐
│           Interface Segregation Principle                        │
│     (Don't force clients to depend on unused methods)            │
└──────────────────────────────────────────────────────────────────┘

BEFORE (Fat Interface):
┌─────────────────────────────────────────┐
│            Worker                       │
│  X Forces all workers to implement      │
│    ALL methods                          │
├─────────────────────────────────────────┤
│ + work()                                │
│ + eat()                                 │
│ + sleep()                               │
│ + manage()     ◄── Robot doesn't manage │
└───────────────┬─────────────────────────┘
                │
        ┌───────┴───────┐
        │               │
        v               v
┌──────────────┐ ┌──────────────┐
│  Developer   │ │    Robot     │  X Robot forced to
├──────────────┤ ├──────────────┤    implement manage()
│ + work()  ✓  │ │ + work()  ✓  │    even though it
│ + eat()   ✓  │ │ + eat()   X  │    doesn't need it
│ + sleep() ✓  │ │ + sleep() X  │
│ + manage() X │ │ + manage() X │
└──────────────┘ └──────────────┘

AFTER (Segregated Interfaces):
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│  Workable    │ │  Feedable    │ │  Manageable  │
├──────────────┤ ├──────────────┤ ├──────────────┤
│ + work()     │ │ + eat()      │ │ + manage()   │
└──────┬───────┘ └──────┬───────┘ └──────┬───────┘
       │                │                │
       │                │                │
       └────────┬───────┴───────┬────────┘
                │               │
                v               v
         ┌──────────────┐ ┌──────────────┐
         │  Developer   │ │   Manager    │
         │ (Workable +  │ │ (Workable +  │
         │  Feedable)   │ │  Feedable +  │
         └──────────────┘ │  Manageable) │
                          └──────────────┘
         ┌──────────────┐
         │    Robot     │  Only implements
         │  (Workable)  │  what it needs!
         └──────────────┘
```

```php
<?php
// BAD: Fat interface - forces implementation of unused methods
interface Worker {
    public function work(): void;
    public function eat(): void;
    public function sleep(): void;
    public function manage(): void;  // Not all workers manage
}

class Developer implements Worker {
    public function work(): void { /* code */ }
    public function eat(): void { /* eat */ }
    public function sleep(): void { /* sleep */ }
    public function manage(): void { /* ??? */ }  // Forced to implement
}

// GOOD: Segregated interfaces
interface Workable {
    public function work(): void;
}

interface Feedable {
    public function eat(): void;
}

interface Manageable {
    public function manage(): void;
}

// Implement only what you need
class Developer implements Workable, Feedable {
    public function work(): void { /* code */ }
    public function eat(): void { /* eat */ }
}

class Manager implements Workable, Feedable, Manageable {
    public function work(): void { /* manage work */ }
    public function eat(): void { /* eat */ }
    public function manage(): void { /* manage team */ }
}

class Robot implements Workable {
    public function work(): void { /* work 24/7 */ }
    // No need to implement eat() or sleep()
}
?>
```

### Dependency Inversion Principle (DIP)

**Definition:** The Dependency Inversion Principle states that high-level modules should not depend on low-level modules; both should depend on abstractions. Furthermore, abstractions should not depend on details; details should depend on abstractions. This is the core principle behind Dependency Injection.

```
┌──────────────────────────────────────────────────────────────────┐
│           Dependency Inversion Principle                         │
│    (Depend on abstractions, not concretions)                     │
└──────────────────────────────────────────────────────────────────┘

BEFORE (High-level depends on low-level):
┌─────────────────────────────────────────┐
│        UserController                   │
│  X Depends on concrete MySQLDatabase    │
├─────────────────────────────────────────┤
│ - db: MySQLDatabase  ◄── Concrete      │
│                         dependency      │
├─────────────────────────────────────────┤
│ + show(id)                              │
└─────────────────────────────────────────┘
                │
                v
┌─────────────────────────────────────────┐
│        MySQLDatabase                    │
├─────────────────────────────────────────┤
│ + query()                               │
│ + insert()                              │
└─────────────────────────────────────────┘
        X Can't easily switch to
          PostgreSQL or mock for testing

AFTER (Both depend on abstraction):
         DatabaseInterface (Abstraction)
         ┌──────────────────┐
         │ + query()        │
         │ + insert()       │
         └────────┬─────────┘
                  │ implements
       ┌──────────┼──────────┐
       │          │          │
       v          v          v
┌──────────┐ ┌──────────┐ ┌──────────┐
│  MySQL   │ │PostgreSQL│ │  Mock    │
│  Database│ │ Database │ │ Database │
├──────────┤ ├──────────┤ ├──────────┤
│+ query() │ │+ query() │ │+ query() │
│+ insert()│ │+ insert()│ │+ insert()│
└──────────┘ └──────────┘ └──────────┘
       ^          ^          ^
       └──────────┴──────────┘
                  │
                  │ can inject any
                  v
         ┌──────────────────┐
         │  UserController  │  Depends on
         │                  │  abstraction!
         ├──────────────────┤
         │ - db: DatabaseInterface
         ├──────────────────┤
         │ + show(id)       │
         └──────────────────┘
```

```php
<?php
// BAD: High-level module depends on low-level module
class UserController {
    private MySQLDatabase $db;  // Depends on concrete implementation
    
    public function __construct() {
        $this->db = new MySQLDatabase();  // Hard-coded dependency
    }
}

// GOOD: Depend on abstractions
interface DatabaseInterface {
    public function query(string $sql): array;
    public function insert(string $table, array $data): int;
}

// Low-level module implements abstraction
class MySQLDatabase implements DatabaseInterface {
    public function query(string $sql): array { /* ... */ }
    public function insert(string $table, array $data): int { /* ... */ }
}

class PostgreSQLDatabase implements DatabaseInterface {
    public function query(string $sql): array { /* ... */ }
    public function insert(string $table, array $data): int { /* ... */ }
}

// High-level module depends on abstraction
class UserController {
    public function __construct(
        private DatabaseInterface $db  // Depends on abstraction
    ) {}
    
    public function show(int $id): array {
        return $this->db->query("SELECT * FROM users WHERE id = {$id}");
    }
}

// Easy to swap implementations
$mysqlController = new UserController(new MySQLDatabase());
$postgresController = new UserController(new PostgreSQLDatabase());
?>
```

---

## 14. PHP 8+ OOP Features

### Definition
**PHP 8+ OOP Features** are modern object-oriented programming enhancements introduced in PHP 8.0 and 8.1 that reduce boilerplate, improve expressiveness, and add powerful new capabilities. Key additions include constructor property promotion, named arguments, match expressions, nullsafe operator, enums, readonly properties, fibers, and union/intersection types — making PHP code more concise and type-safe.

### Constructor Property Promotion

**Definition:** Constructor property promotion (PHP 8.0) simplifies class definitions by allowing properties to be declared, typed, and initialized directly in the constructor parameters. This eliminates the need for separate property declarations and assignments, reducing boilerplate code significantly.

```php
<?php
// PHP 8.0+ - Declare and initialize properties in constructor
class Point {
    public function __construct(
        public float $x = 0.0,
        public float $y = 0.0,
        public float $z = 0.0,
    ) {}
}

$point = new Point(10, 20);
echo $point->x;  // 10

// With readonly (PHP 8.1+)
class ImmutablePoint {
    public function __construct(
        public readonly float $x,
        public readonly float $y
    ) {}
}

$p = new ImmutablePoint(5, 10);
// $p->x = 15;  // ERROR! Readonly property
?>
```

### Named Arguments

**Definition:** Named arguments allow passing arguments to a function based on the parameter name, rather than the position. This makes code self-documenting, allows skipping optional parameters, and is unaffected by changes in the order of parameters in the function signature.

```php
<?php
class HttpClient {
    public function __construct(
        private string $baseUrl,
        private int $timeout = 30,
        private int $retries = 3,
        private array $headers = [],
        private bool $verifySsl = true
    ) {}
}

// Old way - must specify all parameters in order
$client = new HttpClient(
    'https://api.example.com',
    60,
    5,
    ['Authorization' => 'Bearer token'],
    true
);

// PHP 8.0+ - Named arguments (skip optional params, any order)
$client = new HttpClient(
    baseUrl: 'https://api.example.com',
    timeout: 60,
    headers: ['Authorization' => 'Bearer token']
);

// Combined with unpacking
$config = ['timeout' => 45, 'retries' => 2];
$client = new HttpClient('https://api.example.com', ...$config);
?>
```

### Match Expression

**Definition:** The `match` expression is a stricter, more concise version of `switch`. It returns a value, uses strict comparison (`===`), does not require `break` statements (no fall-through), and throws an `UnhandledMatchError` if no condition matches. It is ideal for mapping values or returning results based on conditions.

```php
<?php
class OrderStatus {
    public const PENDING = 'pending';
    public const PAID = 'paid';
    public const SHIPPED = 'shipped';
    public const DELIVERED = 'delivered';
    public const CANCELLED = 'cancelled';
}

class Order {
    public function __construct(private string $status) {}
    
    public function getStatusMessage(): string {
        // Old switch statement
        switch ($this->status) {
            case OrderStatus::PENDING:
                return 'Waiting for payment';
            case OrderStatus::PAID:
                return 'Payment received';
            case OrderStatus::SHIPPED:
            case OrderStatus::DELIVERED:
                return 'Order on its way';
            default:
                return 'Unknown status';
        }
    }
    
    public function getStatusColor(): string {
        // PHP 8.0+ match expression - returns value, strict comparison
        return match($this->status) {
            OrderStatus::PENDING => 'yellow',
            OrderStatus::PAID => 'blue',
            OrderStatus::SHIPPED, OrderStatus::DELIVERED => 'green',
            OrderStatus::CANCELLED => 'red',
            default => 'gray',
        };
    }
    
    public function canCancel(): bool {
        // Match with conditions
        return match(true) {
            $this->status === OrderStatus::PENDING => true,
            $this->status === OrderStatus::PAID => true,
            default => false,
        };
    }
}
?>
```

### Union Types

**Definition:** Union types allow a variable or return type to accept multiple types (e.g., `int|float`). This replaces the need for vague PHPDoc annotations (`@param int|float`) and enforces type safety at runtime, making functions more flexible and explicit about what they accept.

```php
<?php
// PHP 8.0+ - Union types (multiple types allowed)
class Cache {
    private array $data = [];
    
    // Can return int, string, array, or null
    public function get(string $key): int|string|array|null {
        return $this->data[$key] ?? null;
    }
    
    // Can accept multiple types
    public function set(string $key, int|string|array $value): void {
        $this->data[$key] = $value;
    }
    
    // Parameter can be int or float
    public function calculate(int|float $a, int|float $b): int|float {
        return $a + $b;
    }
}

$cache = new Cache();
$cache->set('count', 42);
$cache->set('name', 'John');
$cache->set('items', ['a', 'b', 'c']);
?>
```

### Nullsafe Operator

**Definition:** The nullsafe operator (`?->`) allows accessing properties or methods on an object that might be null. If the object is null, the entire chain returns null immediately instead of throwing an error. This simplifies code by removing nested `if ($obj !== null)` checks.

```php
<?php
class Address {
    public function __construct(private ?string $city = null) {}
    public function getCity(): ?string { return $this->city; }
}

class User {
    public function __construct(private ?Address $address = null) {}
    public function getAddress(): ?Address { return $this->address; }
}

class Order {
    public function __construct(private ?User $user = null) {}
    public function getUser(): ?User { return $this->user; }
}

// Old way - null checks required
function getCityOld(?Order $order): ?string {
    if ($order !== null) {
        $user = $order->getUser();
        if ($user !== null) {
            $address = $user->getAddress();
            if ($address !== null) {
                return $address->getCity();
            }
        }
    }
    return null;
}

// PHP 8.0+ - Nullsafe operator
function getCityNew(?Order $order): ?string {
    return $order?->getUser()?->getAddress()?->getCity();
    // Returns null if any part is null, otherwise the city
}

// Works with methods too
function getCityLength(?Order $order): ?int {
    return $order?->getUser()?->getAddress()?->getCity()?->length();
}
?>
```

### Enums (PHP 8.1+)

**Definition:** Enums (Enumerations) define a custom type restricted to a fixed set of possible values. PHP 8.1 Enums are objects (singleton instances) and can have methods, interfaces, and backed values (int/string). They ensure type safety for states, statuses, or categories where distinct values are required.

```php
<?php
// Basic enum
enum Status {
    case DRAFT;
    case PUBLISHED;
    case ARCHIVED;
}

$postStatus = Status::PUBLISHED;
var_dump($postStatus === Status::PUBLISHED);  // true

// Backed enums (with scalar values)
enum Priority: int {
    case LOW = 1;
    case MEDIUM = 2;
    case HIGH = 3;
    case CRITICAL = 4;
    
    // Methods in enums
    public function label(): string {
        return match($this) {
            self::LOW => 'Low Priority',
            self::MEDIUM => 'Medium Priority',
            self::HIGH => 'High Priority',
            self::CRITICAL => 'Critical Priority',
        };
    }
    
    public function color(): string {
        return match($this) {
            self::LOW => 'gray',
            self::MEDIUM => 'blue',
            self::HIGH => 'orange',
            self::CRITICAL => 'red',
        };
    }
}

$priority = Priority::HIGH;
echo $priority->value;      // 3
echo $priority->label();    // High Priority
echo $priority->color();    // orange

// From value
$fromValue = Priority::from(2);     // Priority::MEDIUM
$tryFrom = Priority::tryFrom(99);   // null (doesn't throw)

// Enum in classes
class Task {
    public function __construct(
        private string $title,
        private Priority $priority = Priority::MEDIUM
    ) {}
    
    public function getPriority(): Priority {
        return $this->priority;
    }
}

$task = new Task('Fix bug', Priority::HIGH);
echo $task->getPriority()->label();  // High Priority

// All cases
foreach (Priority::cases() as $priority) {
    echo "{$priority->name} = {$priority->value}\n";
}
?>
```

### Readonly Classes (PHP 8.2+)

```php
<?php
// PHP 8.2+ - All instance properties are readonly
readonly class Point {
    public function __construct(
        public float $x,
        public float $y
    ) {}
    
    // Static properties can still be modified
    public static int $count = 0;
}

$p = new Point(10, 20);
echo $p->x;  // 10
// $p->x = 15;  // ERROR! Readonly property

// Readonly class with enum
readonly class Config {
    public function __construct(
        public string $appName,
        public string $version,
        public Environment $env  // Enum
    ) {}
}

enum Environment {
    case DEVELOPMENT;
    case STAGING;
    case PRODUCTION;
}

$config = new Config('MyApp', '1.0.0', Environment::PRODUCTION);
// $config->version = '2.0.0';  // ERROR!
?>
```

### Intersection Types (PHP 8.1+)

**Definition:** Intersection types enforce that a value must satisfy **multiple** type constraints simultaneously (e.g., `Countable&Iterator`). Unlike union types ("this OR that"), intersection types mean "this AND that". This is useful when an object must implement multiple interfaces.

```php
<?php
// PHP 8.1+ - Intersection types (must satisfy ALL types)
interface Iterator {
    public function next(): void;
    public function current(): mixed;
}

interface Countable {
    public function count(): int;
}

interface ArrayAccess {
    public function offsetExists($offset): bool;
    public function offsetGet($offset): mixed;
}

// Parameter must implement ALL interfaces
function processCollection(Iterator&Countable&ArrayAccess $collection): void {
    // Can use methods from all three interfaces
    foreach ($collection as $item) {
        // iterate
    }
    
    echo "Count: " . $collection->count();
    
    if (isset($collection[0])) {
        $first = $collection[0];
    }
}

// Union vs Intersection
function example(
    A|B $union,       // Is A OR B
    A&B $intersection // Is A AND B
): void {}
?>
```

### First-Class Callable Syntax (PHP 8.1+)

```php
<?php
class StringManipulator {
    public function uppercase(string $text): string {
        return strtoupper($text);
    }
    
    public static function lowercase(string $text): string {
        return strtolower($text);
    }
}

$manipulator = new StringManipulator();

// Old way
$callback1 = [$manipulator, 'uppercase'];
$callback2 = ['StringManipulator', 'lowercase'];

// PHP 8.1+ - First-class callable syntax
$callback1 = $manipulator->uppercase(...);
$callback2 = StringManipulator::lowercase(...);

// Usage
$texts = ['hello', 'world'];
$result1 = array_map($callback1, $texts);  // ['HELLO', 'WORLD']
$result2 = array_map($callback2, $texts);  // ['hello', 'world']

// With dependency injection
class Processor {
    public function __construct(
        private \Closure $transformer
    ) {}
    
    public function process(string $input): string {
        return ($this->transformer)($input);
    }
}

$processor = new Processor($manipulator->uppercase(...));
echo $processor->process('test');  // TEST
?>
```

---

## 🔑 Key Takeaways

1. **Encapsulation** - Keep data private, expose behavior through methods
2. **Composition over inheritance** - More flexible and testable code
3. **Depend on abstractions** - Use interfaces, not concrete implementations
4. **Single Responsibility** - Each class should have one reason to change
5. **Use PHP 8+ features** - Constructor promotion, named args, match, enums
6. **Favor final classes** - Prevent inheritance unless specifically designed for it
7. **Dependency Injection** - Pass dependencies rather than creating them internally
8. **Static sparingly** - Hard to test, use for true utilities only
9. **Type everything** - Use type declarations for parameters and return types
10. **SOLID principles** - Guide for maintainable, scalable OOP design

---

**Next:** Practice building real-world applications using these OOP principles!
