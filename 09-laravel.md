# 🚀 Laravel - The PHP Framework for Web Artisans

## Summary

This document covers Laravel, a comprehensive PHP framework for web application development. Topics include the request lifecycle and MVC architecture, routing and controllers, Blade templating, database migrations and Eloquent ORM with relationships, request validation, middleware, authentication and authorization systems, file storage, API development with resources, caching strategies, and Livewire for dynamic interfaces.

## Sommaire

- [1. Introduction](#1-introduction)
  - [What is Laravel?](#what-is-laravel)
  - [Request Lifecycle](#request-lifecycle)
  - [MVC Architecture](#mvc-architecture)
  - [Installation](#installation)
  - [Project Structure](#project-structure)
  - [Artisan CLI](#artisan-cli)
  - [Artisan Command Reference](#artisan-command-reference)
- [2. Configuration & Service Container](#2-configuration-&-service-container)
  - [Service Container Architecture](#service-container-architecture)
  - [Configuration Files](#configuration-files)
  - [Environment Variables (.env)](#environment-variables-env)
  - [Service Container](#service-container)
  - [Dependency Injection](#dependency-injection)
  - [Facades](#facades)
  - [Helper Functions](#helper-functions)
- [3. Routing](#3-routing)
  - [Route Definition Architecture](#route-definition-architecture)
  - [Basic Routes](#basic-routes)
  - [Route Parameters](#route-parameters)
  - [Named Routes](#named-routes)
  - [Route Groups](#route-groups)
  - [Resource Routes](#resource-routes)
  - [Route Model Binding](#route-model-binding)
  - [Middleware](#middleware)
- [4. Controllers](#4-controllers)
  - [Controller Structure](#controller-structure)
  - [Creating Controllers](#creating-controllers)
  - [Resource Controllers](#resource-controllers)
  - [Single Action Controllers (Invokable)](#single-action-controllers-invokable)
  - [Dependency Injection](#dependency-injection)
- [5. Views & Blade](#5-views-&-blade)
  - [Blade Template Inheritance](#blade-template-inheritance)
  - [Blade Templating](#blade-templating)
  - [Template Inheritance](#template-inheritance)
  - [Control Structures](#control-structures)
  - [Blade Components](#blade-components)
  - [Blade Directives](#blade-directives)
- [6. Database & Migrations](#6-database-&-migrations)
  - [Migration Workflow](#migration-workflow)
  - [Migrations](#migrations)
  - [Running Migrations](#running-migrations)
  - [Schema Builder](#schema-builder)
  - [Foreign Key Constraints](#foreign-key-constraints)
  - [Seeders](#seeders)
  - [Factories](#factories)
- [7. Eloquent ORM](#7-eloquent-orm)
  - [Eloquent ORM Architecture](#eloquent-orm-architecture)
  - [Models](#models)
  - [CRUD Operations](#crud-operations)
  - [Mass Assignment ($fillable vs $guarded)](#mass-assignment-$fillable-vs-$guarded)
  - [Query Scopes](#query-scopes)
  - [Accessors & Mutators](#accessors-&-mutators)
  - [Collections](#collections)
  - [Pagination](#pagination)
- [8. Eloquent Relationships](#8-eloquent-relationships)
  - [Relationship Types](#relationship-types)
  - [Relationship Types Reference](#relationship-types-reference)
  - [One-to-One](#one-to-one)
  - [One-to-Many](#one-to-many)
  - [Many-to-Many](#many-to-many)
  - [Eager Loading](#eager-loading)
  - [Polymorphic Relations](#polymorphic-relations)
  - [Has Many Through](#has-many-through)
  - [Has One Through](#has-one-through)
- [9. Request & Validation](#9-request-&-validation)
  - [Validation Flow](#validation-flow)
  - [Accessing Request Data](#accessing-request-data)
  - [Validation Rules](#validation-rules)
  - [Form Requests](#form-requests)
  - [Error Messages](#error-messages)
- [10. Middleware](#10-middleware)
  - [Middleware Pipeline](#middleware-pipeline)
  - [Creating Middleware](#creating-middleware)
  - [Before/After Middleware](#before/after-middleware)
  - [Registering Middleware](#registering-middleware)
  - [Terminable Middleware](#terminable-middleware)
- [11. Authentication](#11-authentication)
  - [Authentication Guards & Providers](#authentication-guards-&-providers)
  - [Laravel Breeze](#laravel-breeze)
  - [Laravel Jetstream](#laravel-jetstream)
  - [Registration](#registration)
  - [Login](#login)
  - [Password Reset](#password-reset)
  - [Authentication Usage](#authentication-usage)
  - [Email Verification](#email-verification)
- [12. Authorization](#12-authorization)
  - [Authorization Architecture](#authorization-architecture)
  - [Gates](#gates)
  - [Policies](#policies)
  - [Authorizing Actions](#authorizing-actions)
  - [Blade Directives](#blade-directives)
- [13. File Storage](#13-file-storage)
  - [Storage Architecture](#storage-architecture)
  - [Uploading Files](#uploading-files)
  - [Storage Facade](#storage-facade)
  - [Disks Configuration](#disks-configuration)
  - [Public Disk & URLs](#public-disk-&-urls)
- [14. API Development](#14-api-development)
  - [API Resource Transformation](#api-resource-transformation)
  - [API Routes](#api-routes)
  - [API Resources](#api-resources)
  - [API Responses](#api-responses)
  - [Sanctum Authentication](#sanctum-authentication)
  - [API Best Practices](#api-best-practices)
- [Best Practices Summary](#best-practices-summary)
  - [General](#general)
  - [Database](#database)
  - [Security](#security)
  - [Performance](#performance)
  - [API Development](#api-development)
- [15. Caching](#15-caching)
  - [Cache Drivers](#cache-drivers)
  - [Basic Cache Operations](#basic-cache-operations)
  - [Cache Remember (Most Common Pattern)](#cache-remember-most-common-pattern)
  - [Cache Tags (Redis / Memcached only)](#cache-tags-redis-/-memcached-only)
  - [Query Caching](#query-caching)
  - [Cache Invalidation Strategies](#cache-invalidation-strategies)
  - [HTTP Response Caching](#http-response-caching)
  - [Artisan Cache Commands](#artisan-cache-commands)
  - [Best Practices](#best-practices)
- [16. Livewire](#16-livewire)
  - [Installation](#installation)
  - [Creating a Component](#creating-a-component)
  - [Key Directives](#key-directives)
  - [Real-World Example: Live Search](#real-world-example-live-search)
  - [Validation](#validation)
  - [Lifecycle Hooks](#lifecycle-hooks)
  - [Pagination](#pagination)
  - [Livewire vs. Traditional AJAX](#livewire-vs-traditional-ajax)
  - [Best Practices](#best-practices)



> Laravel is an elegant, expressive PHP framework with an emphasis on developer experience. It provides tools and conventions that make common web development tasks simple and enjoyable.

---

## 1. Introduction

> **Definition:** Laravel is a free, open-source PHP web framework that implements the Model-View-Controller (MVC) architectural pattern. It provides expressive, elegant syntax and a comprehensive ecosystem of tools for building modern web applications, from simple websites to complex enterprise systems.

### What is Laravel?

**Definition:** Laravel is an open-source PHP web framework that follows the Model-View-Controller (MVC) architectural pattern. It prioritizes developer happiness by providing an elegant syntax and robust tools for common tasks like routing, authentication, sessions, and caching, allowing you to build scalable applications quickly.

Laravel is a free, open-source PHP web framework created by Taylor Otwell. It follows the **Model-View-Controller (MVC)** architectural pattern and provides a rich set of features including routing, database abstraction, queue management, and authentication.

**Key Concepts:**
- **Framework:** A structured foundation that provides common functionality and conventions
- **MVC Pattern:** Separation of concerns between data (Model), presentation (View), and logic (Controller)
- **Convention over Configuration:** Sensible defaults reduce the need for extensive configuration
- **Eloquent ORM:** Database interaction through object-oriented syntax
- **Artisan CLI:** Command-line interface for common development tasks

### Request Lifecycle

**Definition:** The Request Lifecycle describes the path an HTTP request takes from entering the application (`public/index.php`) to leaving as a response. It flows through the entry point, HTTP Kernel, Service Providers (bootstrapping), Router, Middleware, and finally the Controller, before returning a response.

Understanding how Laravel processes requests is fundamental to mastering the framework:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         LARAVEL REQUEST LIFECYCLE                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   HTTP Request                                                              │
│        │                                                                    │
│        ▼                                                                    │
│   ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐      │
│   │  public/index   │────▶│  Kernel (HTTP)  │────▶│  Service        │      │
│   │  .php           │     │  Bootstrap      │     │  Providers      │      │
│   │  Entry Point    │     │  Load .env      │     │  Boot Services  │      │
│   └─────────────────┘     │  Load Config    │     └─────────────────┘      │
│                           └─────────────────┘              │                │
│                                                            ▼                │
│                           ┌─────────────────┐     ┌─────────────────┐      │
│                           │  Router         │◄────│  Middleware     │      │
│                           │  Match Route    │     │  Pipeline       │      │
│                           └────────┬────────┘     └─────────────────┘      │
│                                    │                                        │
│                                    ▼                                        │
│                           ┌─────────────────┐                              │
│                           │  Controller     │                              │
│                           │  Handle Request │                              │
│                           └────────┬────────┘                              │
│                                    │                                        │
│                     ┌──────────────┼──────────────┐                        │
│                     ▼              ▼              ▼                        │
│              ┌──────────┐   ┌──────────┐   ┌──────────┐                   │
│              │  Model   │   │  View    │   │ Service  │                   │
│              │  Eloquent│   │  Blade   │   │  Layer   │                   │
│              │  Query   │   │  Render  │   │  Logic   │                   │
│              └────┬─────┘   └────┬─────┘   └────┬─────┘                   │
│                   │              │              │                          │
│                   └──────────────┼──────────────┘                          │
│                                  ▼                                         │
│                           ┌─────────────────┐                              │
│                           │  Response       │                              │
│                           │  Middleware     │                              │
│                           └────────┬────────┘                              │
│                                    │                                        │
│                                    ▼                                        │
│                              HTTP Response                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Lifecycle Stages:**
1. **Entry Point** - `public/index.php` receives the HTTP request
2. **Kernel Bootstrap** - Application kernel initializes, loads configuration
3. **Service Providers** - Boot services, register bindings
4. **Middleware Pipeline** - Process request through middleware stack
5. **Routing** - Match request to defined route
6. **Controller Execution** - Business logic execution
7. **Model/View Interaction** - Data retrieval and view rendering
8. **Response** - Return HTTP response to client

**Key Features:**
- **Elegant syntax** - Expressive, readable code
- **MVC architecture** - Separation of concerns
- **Eloquent ORM** - Beautiful database interactions
- **Blade templating** - Powerful, intuitive templates
- **Artisan CLI** - Command-line tools for development
- **Robust ecosystem** - Packages, tools, and community support

### MVC Architecture

Laravel follows the **Model-View-Controller** pattern:

```
┌─────────────────────────────────────────────────────────┐
│                      REQUEST                            │
│                         │                               │
│                         ▼                               │
│                ┌────────────────┐                       │
│                │    ROUTES      │                       │
│                └────────┬───────┘                       │
│                         │                               │
│                         ▼                               │
│                ┌────────────────┐                       │
│                │  CONTROLLER    │ ◄── Business logic    │
│                └───────┬────────┘                       │
│                ┌───────┴────────┐                       │
│                ▼                ▼                       │
│         ┌──────────┐    ┌──────────┐                   │
│         │  MODEL   │    │   VIEW   │                   │
│         │ (Data)   │    │ (Blade)  │                   │
│         └──────────┘    └────┬─────┘                   │
│                              │                          │
│                              ▼                          │
│                         RESPONSE                        │
└─────────────────────────────────────────────────────────┘
```

**Components:**

| Component | Responsibility | Example |
|-----------|---------------|---------|
| **Model** | Data layer, business logic | `User.php` - defines User data and relationships |
| **View** | Presentation layer | `resources/views/users/index.blade.php` |
| **Controller** | Handle requests, coordinate | `UserController.php` - process and return views |

### Installation

**Requirements:**
- PHP >= 8.1
- Composer
- MySQL/PostgreSQL/SQLite
- Node.js & NPM (for frontend assets)

**Option 1: Via Composer (Recommended)**

```bash
# Create new Laravel project
composer create-project laravel/laravel my-app

# Or with specific version
composer create-project laravel/laravel:^11.0 my-app

# Navigate to project
cd my-app

# Start development server
php artisan serve
```

**Option 2: Via Laravel Installer**

```bash
# Install Laravel installer globally
composer global require laravel/installer

# Create new project
laravel new my-app

# Start with specific stack
laravel new my-app --jet  # With Jetstream
laravel new my-app --breeze  # With Breeze
```

**Option 3: Via Laravel CLI**

```bash
# Using the official CLI tool
curl -s https://laravel.build/my-app | bash

# With specific PHP version
curl -s "https://laravel.build/my-app?php=82" | bash
```

### Project Structure

**Definition:** Laravel enforces a standard directory structure to organize code. The `app/` directory contains the core logic (Controllers, Models), `resources/` holds views and assets, `routes/` defines URL endpoints, `database/` manages migrations/seeders, and `config/` centralizes configuration files. This convention-over-configuration approach speeds up development.

```
my-app/
├── app/                          # Application core
│   ├── Http/
│   │   ├── Controllers/         # Controller classes
│   │   ├── Middleware/          # HTTP middleware
│   │   └── Requests/            # Form request validation
│   ├── Models/                  # Eloquent models
│   ├── Providers/               # Service providers
│   └── Console/                 # Artisan commands
├── bootstrap/                   # Application bootstrapping
├── config/                      # Configuration files
├── database/
│   ├── factories/               # Model factories
│   ├── migrations/              # Database migrations
│   └── seeders/                 # Database seeders
├── public/                      # Web server root
│   ├── index.php               # Application entry point
│   └── assets/                 # Compiled assets
├── resources/
│   ├── views/                  # Blade templates
│   ├── css/                    # CSS files
│   └── js/                     # JavaScript files
├── routes/
│   ├── web.php                 # Web routes
│   ├── api.php                 # API routes
│   └── console.php             # Console routes
├── storage/                     # Logs, cache, compiled views
├── tests/                       # Automated tests
├── .env                        # Environment variables
├── artisan                     # Artisan CLI
└── composer.json               # PHP dependencies
```

**Key Directories Explained:**

| Directory | Purpose |
|-----------|---------|
| `app/Http/Controllers` | Handle HTTP requests, return responses |
| `app/Models` | Eloquent models, database interactions |
| `database/migrations` | Database schema version control |
| `resources/views` | Blade template files |
| `routes/web.php` | Web application routes |
| `config/` | Configuration files for all services |

### Artisan CLI

**Definition:** Artisan is the command-line interface included with Laravel. It provides various helpful commands for your application, such as generating boilerplate code (controllers, models), running migrations, flushing cache, and managing the application state (`php artisan serve`).

Artisan is Laravel's command-line interface. It provides dozens of helpful commands.

**Common Commands:**

```bash
# Development server
php artisan serve
php artisan serve --port=8080

# Application status
php artisan about
php artisan optimize
php artisan cache:clear

# Code generation
### Artisan Command Reference

| Command | Description | Use Case |
|---------|-------------|----------|
| `php artisan serve` | Start dev server | Run app locally at `localhost:8000` |
| `php artisan migrate` | Run migrations | Update database schema |
| `php artisan make:model` | Create Model | Add new Eloquent model |
| `php artisan make:controller` | Create Controller | Add new HTTP controller |
| `php artisan make:migration` | Create Migration | Add new database migration file |
| `php artisan route:list` | List routes | View all registered routes |
| `php artisan tinker` | REPL | Interact with app via command line |
| `php artisan key:generate` | Generate App Key | Secure session/encrypted data |
| `php artisan optimize:clear` | Clear Cache | Remove all cached views/configs |

```bash
# Code generation examples
php artisan make:controller UserController
php artisan make:model Post -mcr  # Model + Migration + Controller + Resource
php artisan make:middleware CheckRole
```

# Cache and optimization
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear

# Maintenance mode
php artisan down
php artisan up

# Interactive shell
php artisan tinker
```

**Creating Custom Commands:**

```bash
php artisan make:command SendReminderEmails
```

```php
<?php
// app/Console/Commands/SendReminderEmails.php

namespace App\Console\Commands;

use Illuminate\Console\Command;

class SendReminderEmails extends Command
{
    // Command signature
    protected $signature = 'emails:send-reminders {--user= : Specific user ID}';

    // Command description
    protected $description = 'Send reminder emails to users';

    public function handle(): void
    {
        $userId = $this->option('user');
        
        if ($userId) {
            $this->info("Sending reminder to user: {$userId}");
        } else {
            $this->info('Sending reminders to all users...');
        }
        
        // Command logic here
        
        $this->info('Reminders sent successfully!');
        return Command::SUCCESS;
    }
}
```

---

## 2. Configuration & Service Container

> **Definition:** The Configuration system provides environment-based settings management, while the Service Container is Laravel's powerful dependency injection container that manages class dependencies and performs automatic resolution.

### Service Container Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      SERVICE CONTAINER ARCHITECTURE                         │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │                      SERVICE CONTAINER                           │     │
│   │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │     │
│   │  │   Bindings   │  │  Singletons  │  │   Instances  │           │     │
│   │  │  (Transient) │  │  (One Time)  │  │  (Concrete)  │           │     │
│   │  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘           │     │
│   │         │                 │                 │                    │     │
│   │         └─────────────────┼─────────────────┘                    │     │
│   │                           ▼                                       │     │
│   │  ┌─────────────────────────────────────────────────────────────┐ │     │
│   │  │                    RESOLUTION LOGIC                          │ │     │
│   │  │  1. Check if concrete binding exists                        │ │     │
│   │  │  2. Use reflection to inspect class constructor             │ │     │
│   │  │  3. Auto-resolve dependencies recursively                   │ │     │
│   │  │  4. Instantiate and return                                 │ │     │
│   │  └─────────────────────────────────────────────────────────────┘ │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                    │                                        │
│                                    ▼                                        │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              DEPENDENCY INJECTION FLOW                           │     │
│   │                                                                  │     │
│   │   Constructor Injection        Method Injection                  │     │
│   │   ┌──────────────────┐        ┌──────────────────┐              │     │
│   │   │ Controller       │        │ Route Closure    │              │     │
│   │   │ ┌──────────────┐ │        │ ┌──────────────┐ │              │     │
│   │   │ │ __construct()│ │        │ │ handle()     │ │              │     │
│   │   │ │ UserService  │ │        │ │ UserService  │ │              │     │
│   │   │ └──────┬───────┘ │        │ └──────┬───────┘ │              │     │
│   │   │        │         │        │        │         │              │     │
│   │   │   Auto-Resolved  │        │   Auto-Resolved  │              │     │
│   │   └────────┼─────────┘        └────────┼─────────┘              │     │
│   │            │                           │                        │     │
│   │            └───────────┬───────────────┘                        │     │
│   │                        ▼                                         │     │
│   │   ┌──────────────────────────────────────────────────┐          │     │
│   │   │              UserService Instantiated            │          │     │
│   │   │         (Dependencies resolved recursively)      │          │     │
│   │   └──────────────────────────────────────────────────┘          │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Configuration Files

Laravel stores configuration in PHP files within the `config/` directory.

**Environment-Based Configuration:**

```php
// config/app.php
return [
    'name' => env('APP_NAME', 'Laravel'),
    'env' => env('APP_ENV', 'production'),
    'debug' => env('APP_DEBUG', false),
    'url' => env('APP_URL', 'http://localhost'),
    'timezone' => 'UTC',
    'locale' => 'en',
    
    // Service providers
    'providers' => [
        // ...
    ],
];
```

**Accessing Configuration:**

```php
<?php
// Get configuration value
$name = config('app.name');
$debug = config('app.debug');

// With default value
$fallback = config('services.stripe.secret', 'default_value');

// Set configuration at runtime
config(['app.timezone' => 'America/New_York']);
```

### Environment Variables (.env)

**Definition:** The `.env` file handles application configuration that varies across environments (local, staging, production), such as database credentials and debug modes. Laravel uses the DotEnv library to load these variables into the `$_ENV` superglobal and the config system (`config()`).

The `.env` file contains environment-specific variables and should NEVER be committed to version control.

```env
# .env
APP_NAME="My Laravel App"
APP_ENV=local
APP_KEY=base64:your-key-here
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel_app
DB_USERNAME=root
DB_PASSWORD=secret

MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
```

**Accessing Environment Variables:**

```php
<?php
use Illuminate\Support\Facades\Env;

// Get environment variable
$env = env('APP_ENV');
$debug = env('APP_DEBUG', false); // With default

// Using Env facade (recommended for production)
$appName = Env::get('APP_NAME');
```

**Environment Files:**
- `.env` - Local development
- `.env.testing` - Testing environment
- `.env.production` - Production (don't store locally)

### Service Container

**Definition:** The Service Container is a powerful tool for managing class dependencies and performing dependency injection. It acts as a registry where you "bind" classes or interfaces and their creation logic, allowing Laravel to automatically resolve and inject them wherever they are needed.

The service container is a powerful tool for managing class dependencies and performing dependency injection.

**Binding to Container:**

```php
<?php
use App\Services\PaymentGateway;
use App\Services\StripePayment;

// Simple binding
app()->bind(PaymentGateway::class, function ($app) {
    return new StripePayment(config('services.stripe.secret'));
});

// Singleton (same instance every time)
app()->singleton(PaymentGateway::class, function ($app) {
    return new StripePayment(config('services.stripe.secret'));
});

// Scoped (singleton within request lifecycle)
app()->scoped(PaymentGateway::class, function ($app) {
    return new StripePayment(config('services.stripe.secret'));
});

// Instance binding
$gateway = new StripePayment('secret');
app()->instance(PaymentGateway::class, $gateway);
```

**Resolving from Container:**

```php
<?php
// Using app() helper
$gateway = app(PaymentGateway::class);

// Using resolve() helper
$gateway = resolve(PaymentGateway::class);

// Using dependency injection in constructor
class OrderController extends Controller
{
    public function __construct(
        private PaymentGateway $payment
    ) {}
}

// Automatic resolution
$controller = app()->make(OrderController::class);
```

### Dependency Injection

**Definition:** Dependency Injection (DI) in Laravel is primarily handled by the Service Container. Instead of creating objects manually (using `new Class()`), you type-hint dependencies in a class constructor or method (like a Controller actions), and the Container automatically resolves and injects them.

Laravel's container automatically resolves dependencies.

**Constructor Injection:**

```php
<?php
namespace App\Http\Controllers;

use App\Services\PaymentGateway;
use App\Repositories\OrderRepository;

class OrderController extends Controller
{
    public function __construct(
        private PaymentGateway $payment,
        private OrderRepository $orders
    ) {}

    public function store(Request $request): RedirectResponse
    {
        // Dependencies automatically injected
        $order = $this->orders->create($request->validated());
        $this->payment->process($order);
        
        return redirect()->route('orders.index');
    }
}
```

**Method Injection:**

```php
<?php
public function update(
    Request $request,
    OrderRepository $orders,
    int $id
): RedirectResponse {
    $orders->update($id, $request->validated());
    return redirect()->back();
}
```

**Interface Binding:**

```php
<?php
// app/Providers/AppServiceProvider.php
use App\Contracts\PaymentGateway;
use App\Services\StripePayment;

public function register(): void
{
    $this->app->bind(PaymentGateway::class, StripePayment::class);
}

// Usage - Laravel injects StripePayment automatically
class OrderController extends Controller
{
    public function __construct(
        private PaymentGateway $payment
    ) {}
}
```

### Facades

**Definition:** Facades provide a static interface to classes that are available in the application's service container. They act as "static proxies" to underlying instance methods, offering a terse, expressive syntax (e.g., `Route::get()`, `Cache::put()`) without requiring manual dependency injection, though they can obscure dependencies.

Facades provide a static-like interface to classes in the service container.

```php
<?php
use Illuminate\Support\Facades\Cache;
use Illuminate\Support\Facades\DB;
use Illuminate\Support\Facades\Storage;
use Illuminate\Support\Facades\Mail;

// Using Cache facade
Cache::put('key', 'value', 3600);
$value = Cache::get('key', 'default');

// Using DB facade
$users = DB::table('users')->get();

// Using Storage facade
Storage::put('file.txt', 'content');
$content = Storage::get('file.txt');

// Using Mail facade
Mail::to($user)->send(new WelcomeMail($user));
```

**Common Facades:**

| Facade | Accesses | Example |
|--------|----------|---------|
| `Auth` | Authentication | `Auth::user()` |
| `Cache` | Caching | `Cache::get('key')` |
| `Config` | Configuration | `Config::get('app.name')` |
| `DB` | Database | `DB::table('users')` |
| `Hash` | Hashing | `Hash::make('password')` |
| `Log` | Logging | `Log::info('message')` |
| `Route` | Routing | `Route::get('/users')` |
| `Session` | Sessions | `Session::get('key')` |
| `Storage` | File storage | `Storage::put('file', 'content')` |
| `Validator` | Validation | `Validator::make($data, $rules)` |

### Helper Functions

**Definition:** Laravel includes a variety of global "helper" PHP functions (like `dd()`, `url()`, `config()`, `view()`) that provide convenient shortcuts to common framework features. They are available globally and do not require importing any classes.

Laravel provides many global helper functions.

**Common Helpers:**

```php
<?php
// Application
app();                    // Get container instance
config('app.name');       // Get config value
env('APP_ENV');          // Get env variable

// Arrays
array_add($array, 'key', 'value');
array_first($array, function ($value) {
    return $value > 10;
});
head($array);            // First element
last($array);            // Last element

// Paths
base_path();             // /var/www/my-app
app_path();              // /var/www/my-app/app
config_path();           // /var/www/my-app/config
public_path();           // /var/www/my-app/public
resource_path();         // /var/www/my-app/resources
storage_path();          // /var/www/my-app/storage

// Strings
str_contains('hello', 'ell');    // true
str_starts_with('hello', 'he');  // true
str_ends_with('hello', 'lo');    // true
Str::slug('Hello World');        // 'hello-world'
Str::random(32);                 // Random string

// URLs
url('/users');           // http://localhost/users
route('users.index');    // Named route URL
asset('css/app.css');    // http://localhost/css/app.css

// Authentication
auth()->user();          // Current user
auth()->check();         // Is user authenticated?
auth()->guest();         // Is user a guest?

// Request
request()->input('name');
request()->all();
request()->has('email');

// Response
response()->json(['key' => 'value']);
response()->view('view.name', $data);
response()->download($path, $name);
```

---

## 3. Routing

> **Definition:** Routing maps HTTP requests to specific controller actions or closures. Laravel's router matches the incoming request URI and HTTP method to defined routes, then dispatches the appropriate handler.

### Route Definition Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        ROUTE DEFINITION TYPES                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │                     ROUTE REGISTRY                               │     │
│   │                                                                  │     │
│   │   HTTP Verb    URI Pattern         Action        Name           │     │
│   │   ────────────────────────────────────────────────────────────  │     │
│   │   GET         /users              index()       users.index     │     │
│   │   GET         /users/create       create()      users.create    │     │
│   │   POST        /users              store()       users.store     │     │
│   │   GET         /users/{id}         show()        users.show      │     │
│   │   GET         /users/{id}/edit    edit()        users.edit      │     │
│   │   PUT/PATCH   /users/{id}         update()      users.update    │     │
│   │   DELETE      /users/{id}         destroy()     users.destroy   │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │                    ROUTE GROUPS HIERARCHY                        │     │
│   │                                                                  │     │
│   │   Route::middleware(['auth'])                                    │     │
│   │       └── Route::prefix('admin')                                 │     │
│   │           └── Route::controller(AdminController::class)          │     │
│   │               ├── Route::get('/dashboard', 'dashboard')          │     │
│   │               ├── Route::get('/users', 'users')                  │     │
│   │               └── Route::post('/settings', 'settings')           │     │
│   │                                                                  │     │
│   │   Results in:                                                    │     │
│   │   /admin/dashboard  (auth middleware)                            │     │
│   │   /admin/users      (auth middleware)                            │     │
│   │   /admin/settings   (auth middleware)                            │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Basic Routes

**Definition:** Routing directs incoming HTTP requests to specific code handlers (closures or controllers) based on the URL path and HTTP method (GET, POST, etc.). All routes are defined in the `routes/` directory (typically `client-facing in web.php` and API in `api.php`).

Routes are defined in `routes/web.php` (web) or `routes/api.php` (API).

```php
<?php
use Illuminate\Support\Facades\Route;

// Basic GET route
Route::get('/', function () {
    return view('welcome');
});

// Return view directly
Route::view('/about', 'pages.about');

// Return redirect
Route::redirect('/old-url', '/new-url', 301);

// All HTTP verbs
Route::get('/users', [UserController::class, 'index']);
Route::post('/users', [UserController::class, 'store']);
Route::put('/users/{id}', [UserController::class, 'update']);
Route::patch('/users/{id}', [UserController::class, 'update']);
Route::delete('/users/{id}', [UserController::class, 'destroy']);

// Multiple verbs
Route::match(['get', 'post'], '/users', [UserController::class, 'handle']);
Route::any('/users', [UserController::class, 'handle']); // All HTTP verbs

// Fallback route (404)
Route::fallback(function () {
    return view('errors.404');
});
```

### Route Parameters

**Definition:** Route parameters allow you to capture segments of the URI within your route definition (e.g., `/user/{id}`). These captured values are passed as arguments to your route callback or controller method, enabling dynamic pages based on IDs or slugs.

```php
<?php
// Required parameter
Route::get('/users/{id}', function (string $id) {
    return "User ID: {$id}";
});

// Multiple parameters
Route::get('/users/{id}/posts/{postId}', function (string $id, string $postId) {
    return "User: {$id}, Post: {$postId}";
});

// Optional parameter (with default)
Route::get('/users/{id?}', function (?string $id = null) {
    return $id ? "User: {$id}" : "All users";
});

// Regular expression constraints
Route::get('/users/{id}', function (string $id) {
    return "User: {$id}";
})->where('id', '[0-9]+');

// Multiple constraints
Route::get('/users/{name}/{id}', function (string $name, int $id) {
    // ...
})->where([
    'name' => '[a-z]+',
    'id' => '[0-9]+'
]);

// Global patterns (in RouteServiceProvider)
public function boot(): void
{
    Route::pattern('id', '[0-9]+');
}
```

### Named Routes

**Definition:** Named routes allow you to assign a specific name to a route path (using `->name('profile')`). This decouples the URL structure from the code; you can generate URLs or redirects using the name (`route('profile')`) so changing the path later doesn't break the application.

```php
<?php
// Define named route
Route::get('/users/profile', [UserController::class, 'profile'])
    ->name('user.profile');

// Generate URL
$url = route('user.profile');  // /users/profile

// With parameters
Route::get('/users/{id}/edit', [UserController::class, 'edit'])
    ->name('user.edit');

$url = route('user.edit', ['id' => 5]);  // /users/5/edit

// Generate redirect
return redirect()->route('user.profile');

// Check current route
if (request()->routeIs('user.*')) {
    // Current route starts with 'user.'
}
```

### Route Groups

**Definition:** Route groups allow you to share route attributes, such as middleware, namespaces, or path prefixes, across a large number of routes without needing to define those attributes on each individual route. This keeps route files organized and DRY (Don't Repeat Yourself).

```php
<?php
// Middleware group
Route::middleware(['auth', 'verified'])->group(function () {
    Route::get('/dashboard', [DashboardController::class, 'index']);
    Route::get('/settings', [SettingsController::class, 'index']);
});

// Controller group
Route::controller(UserController::class)->group(function () {
    Route::get('/users', 'index');
    Route::get('/users/create', 'create');
    Route::post('/users', 'store');
});

// Prefix group
Route::prefix('admin')->group(function () {
    Route::get('/users', [AdminController::class, 'users']);
    Route::get('/posts', [AdminController::class, 'posts']);
});
// Results in: /admin/users, /admin/posts

// Name prefix
Route::name('admin.')->group(function () {
    Route::get('/users', [AdminController::class, 'users'])->name('users');
});
// Route name: admin.users

// Subdomain routing
Route::domain('{account}.myapp.com')->group(function () {
    Route::get('/', function (string $account) {
        return "Account: {$account}";
    });
});

// Namespace group
Route::namespace('App\Http\Controllers\Admin')->group(function () {
    Route::get('/admin/users', 'UserController@index');
});
```

### Resource Routes

**Definition:** Resource routing assigns the typical "CRUD" routes to a controller with a single line of code (`Route::resource('photos', PhotoController::class)`). This automatically creates routes for index, create, store, show, edit, update, and destroy actions following RESTful conventions.

```php
<?php
// Full resource routes
Route::resource('posts', PostController::class);

// Generates:
// GET    /posts          -> index()
// GET    /posts/create   -> create()
// POST   /posts          -> store()
// GET    /posts/{post}   -> show()
// GET    /posts/{post}/edit -> edit()
// PUT    /posts/{post}   -> update()
// DELETE /posts/{post}   -> destroy()

// Partial resource
Route::resource('posts', PostController::class)->only(['index', 'show']);
Route::resource('posts', PostController::class)->except(['create', 'store']);

// API resource (no create/edit forms)
Route::apiResource('posts', PostController::class);

// Nested resources
Route::resource('posts.comments', CommentController::class);
// Generates: /posts/{post}/comments/{comment}

// Shallow nesting (recommended for deep nesting)
Route::resource('posts.comments', CommentController::class)->shallow();
// Generates: /posts/{post}/comments and /comments/{comment}
```

### Route Model Binding

**Definition:** Route model binding automatically injects model instances into your routes based on the ID present in the URI. For example, typing `(User $user)` instead of `($id)` tells Laravel to automatically fetch the User model with that ID from the database, or 404 if not found.

```php
<?php
// Implicit binding (automatic resolution)
Route::get('/posts/{post}', function (Post $post) {
    return $post; // Automatically fetches Post where id = {post}
});

// Custom key (route model binding with slug)
Route::get('/posts/{post:slug}', function (Post $post) {
    return $post; // Fetches by slug instead of id
});

// Customize in model
class Post extends Model
{
    public function getRouteKeyName(): string
    {
        return 'slug';
    }
}

// Explicit binding (in RouteServiceProvider)
public function boot(): void
{
    Route::bind('post', function ($value) {
        return Post::where('slug', $value)
            ->where('published', true)
            ->firstOrFail();
    });
}

// Scoped binding (child route)
Route::get('/users/{user}/posts/{post:slug}', function (User $user, Post $post) {
    return $post; // Ensures post belongs to user
});
```

### Middleware

**Definition:** Middleware provide a convenient mechanism for inspecting and filtering HTTP requests entering your application. Common uses include authenticating users (`auth`), verifying CSRF tokens, logging, or trimming strings. They act as layers the request must pass through before reaching the core logic.

```php
<?php
// Apply middleware to route
Route::get('/admin', [AdminController::class, 'index'])
    ->middleware('auth');

// Multiple middleware
Route::get('/dashboard', [DashboardController::class, 'index'])
    ->middleware(['auth', 'verified', 'role:admin']);

// Middleware groups
Route::middleware(['web', 'auth'])->group(function () {
    // All routes have web and auth middleware
});

// Without middleware (for routes in group)
Route::get('/public', [PublicController::class, 'index'])
    ->withoutMiddleware(['auth']);
```

---

## 4. Controllers

> **Definition:** Controllers are classes that organize request handling logic into discrete units. They receive HTTP requests from the router, process business logic, interact with models, and return responses (views, redirects, or JSON).

### Controller Structure

**Definition:** Controllers group related request handling logic into a single class. Instead of defining all request handling logic as closures in route files, you organize behavior into methods (actions) like `index()`, `show()`, `store()`. Controllers are stored in `app/Http/Controllers`.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      CONTROLLER ARCHITECTURE                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │                    BaseController                                │     │
│   │  ┌──────────────────────────────────────────────────────────┐   │     │
│   │  │  Common functionality:                                   │   │     │
│   │  │  - Middleware management                                 │   │     │
│   │  │  - Authorization helpers                                 │   │     │
│   │  │  - Response utilities                                    │   │     │
│   │  └──────────────────────────────────────────────────────────┘   │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                  ▲                                          │
│                                  │                                          │
│        ┌─────────────────────────┼─────────────────────────┐               │
│        │                         │                         │               │
│        ▼                         ▼                         ▼               │
│   ┌──────────┐            ┌──────────┐            ┌──────────┐            │
│   │ Resource │            │ Regular  │            │ Invokable│            │
│   │Controller│            │Controller│            │Controller│            │
│   ├──────────┤            ├──────────┤            ├──────────┤            │
│   │index()   │            │custom()  │            │__invoke()│            │
│   │create()  │            │actions   │            │         │            │
│   │store()   │            │          │            │ Single   │            │
│   │show()    │            │          │            │ Action   │            │
│   │edit()    │            │          │            │          │            │
│   │update()  │            │          │            │          │            │
│   │destroy() │            │          │            │          │            │
│   └──────────┘            └──────────┘            └──────────┘            │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              CONTROLLER REQUEST FLOW                             │     │
│   │                                                                  │     │
│   │   Route ──▶ Controller ──▶ Validation ──▶ Business Logic        │     │
│   │                                  │                              │     │
│   │                                  ▼                              │     │
│   │                         ┌──────────────┐                       │     │
│   │                         │   Model      │                       │     │
│   │                         │   Eloquent   │                       │     │
│   │                         └──────┬───────┘                       │     │
│   │                                │                               │     │
│   │                                ▼                               │     │
│   │                         ┌──────────────┐                       │     │
│   │                         │   View /     │                       │     │
│   │                         │   Response   │                       │     │
│   │                         └──────────────┘                       │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Creating Controllers

**Definition:** You typically create controllers using the Artisan CLI command `php artisan make:controller`. This generates the class file with the correct namespace and inheritance. You can create plain controllers, resource controllers (`--resource`), or API controllers (`--api`).

```bash
# Create controller
php artisan make:controller UserController

# Create API controller (no create/edit methods)
php artisan make:controller Api/UserController --api

# Create with resource methods
php artisan make:controller PostController --resource

# Create invokable controller (single action)
php artisan make:controller ShowPostController --invokable
```

**Basic Controller:**

```php
<?php
namespace App\Http\Controllers;

use App\Models\User;
use Illuminate\Http\Request;
use Illuminate\View\View;

class UserController extends Controller
{
    // List all users
    public function index(): View
    {
        $users = User::paginate(10);
        return view('users.index', compact('users'));
    }

    // Show create form
    public function create(): View
    {
        return view('users.create');
    }

    // Store new user
    public function store(Request $request): RedirectResponse
    {
        $validated = $request->validate([
            'name' => 'required|string|max:255',
            'email' => 'required|email|unique:users',
            'password' => 'required|min:8|confirmed',
        ]);

        User::create($validated);

        return redirect()->route('users.index')
            ->with('success', 'User created successfully!');
    }

    // Show single user
    public function show(User $user): View
    {
        return view('users.show', compact('user'));
    }

    // Show edit form
    public function edit(User $user): View
    {
        return view('users.edit', compact('user'));
    }

    // Update user
    public function update(Request $request, User $user): RedirectResponse
    {
        $validated = $request->validate([
            'name' => 'required|string|max:255',
            'email' => 'required|email|unique:users,email,' . $user->id,
        ]);

        $user->update($validated);

        return redirect()->route('users.index')
            ->with('success', 'User updated successfully!');
    }

    // Delete user
    public function destroy(User $user): RedirectResponse
    {
        $user->delete();

        return redirect()->route('users.index')
            ->with('success', 'User deleted successfully!');
    }
}
```

### Resource Controllers

**Definition:** A Resource Controller contains methods for each of the available resource operations (index, create, store, show, edit, update, destroy). It pairs perfectly with `Route::resource()` to provide a standardized structure for CRUD functionality.

```php
<?php
// app/Http/Controllers/PostController.php

namespace App\Http\Controllers;

use App\Models\Post;
use Illuminate\Http\Request;

class PostController extends Controller
{
    // Display a listing of posts
    public function index()
    {
        $posts = Post::with('author')
            ->latest()
            ->paginate(10);
        
        return view('posts.index', compact('posts'));
    }

    // Show the form for creating a new post
    public function create()
    {
        return view('posts.create');
    }

    // Store a newly created post
    public function store(Request $request)
    {
        $validated = $request->validate([
            'title' => 'required|max:255',
            'content' => 'required',
            'published_at' => 'nullable|date',
        ]);

        $post = auth()->user()->posts()->create($validated);

        return redirect()->route('posts.show', $post)
            ->with('success', 'Post created!');
    }

    // Display the specified post
    public function show(Post $post)
    {
        return view('posts.show', compact('post'));
    }

    // Show the form for editing the specified post
    public function edit(Post $post)
    {
        $this->authorize('update', $post);
        return view('posts.edit', compact('post'));
    }

    // Update the specified post
    public function update(Request $request, Post $post)
    {
        $this->authorize('update', $post);

        $validated = $request->validate([
            'title' => 'required|max:255',
            'content' => 'required',
        ]);

        $post->update($validated);

        return redirect()->route('posts.show', $post)
            ->with('success', 'Post updated!');
    }

    // Remove the specified post
    public function destroy(Post $post)
    {
        $this->authorize('delete', $post);
        
        $post->delete();

        return redirect()->route('posts.index')
            ->with('success', 'Post deleted!');
    }
}
```

### Single Action Controllers (Invokable)

**Definition:** If a controller action is particularly complex or doesn't fit the standard CRUD resource pattern, you can define a "Single Action Controller" by implementing the `__invoke` method. You can then route to the controller itself without specifying a method name.

```php
<?php
// app/Http/Controllers/ProcessPaymentController.php

namespace App\Http\Controllers;

use App\Services\PaymentService;
use Illuminate\Http\Request;

class ProcessPaymentController extends Controller
{
    public function __construct(
        private PaymentService $paymentService
    ) {}

    // Single __invoke method
    public function __invoke(Request $request)
    {
        $validated = $request->validate([
            'amount' => 'required|numeric|min:1',
            'currency' => 'required|string|size:3',
        ]);

        $result = $this->paymentService->process($validated);

        return response()->json([
            'success' => true,
            'transaction_id' => $result->id,
        ]);
    }
}
```

```php
<?php
// routes/web.php
Route::post('/payment', ProcessPaymentController::class);
```

### Dependency Injection

**Definition:** You can type-hint dependencies in a Controller's constructor or method signature. The service container creates the controller instance and resolves all type-hinted dependencies automatically. Method injection is particularly useful for route-specific dependencies like `Request` or Models.

```php
<?php
namespace App\Http\Controllers;

use App\Repositories\UserRepository;
use App\Services\EmailService;
use Illuminate\Http\Request;

class UserController extends Controller
{
    // Constructor injection
    public function __construct(
        private UserRepository $users,
        private EmailService $email
    ) {}

    // Method injection
    public function store(
        Request $request,
        UserRepository $users
    ): RedirectResponse {
        $user = $users->create($request->validated());
        
        $this->email->sendWelcome($user);
        
        return redirect()->back();
    }
}
```

---

## 5. Views & Blade

> **Definition:** Views are the presentation layer of Laravel applications. Blade is Laravel's templating engine that provides an elegant syntax for combining PHP logic with HTML, including template inheritance, components, and control structures.

### Blade Template Inheritance

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      BLADE TEMPLATE INHERITANCE                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │                    MASTER LAYOUT                                 │     │
│   │  (resources/views/layouts/app.blade.php)                         │     │
│   │                                                                  │     │
│   │  <!DOCTYPE html>                                                 │     │
│   │  <html>                                                          │     │
│   │  <head>                                                          │     │
│   │      <title>@yield('title')</title>         ◄── Section 1       │     │
│   │      @stack('styles')                       ◄── Stack           │     │
│   │  </head>                                                         │     │
│   │  <body>                                                          │     │
│   │      @yield('content')                      ◄── Section 2       │     │
│   │      @section('scripts')                    ◄── Section 3       │     │
│   │          <script src="/app.js"></script>                         │     │
│   │      @show                                                       │     │
│   │  </body>                                                         │     │
│   │  </html>                                                         │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                  ▲                                          │
│                                  │ extends('layouts.app')                   │
│                    ┌─────────────┴─────────────┐                           │
│                    │                             │                           │
│                    ▼                             ▼                           │
│   ┌────────────────────────┐    ┌────────────────────────┐                  │
│   │     CHILD VIEW 1       │    │     CHILD VIEW 2       │                  │
│   │   (users/index)        │    │   (users/create)       │                  │
│   │                        │    │                        │                  │
│   │   @section('title')    │    │   @section('title')    │                  │
│   │       Users List       │    │       Create User      │                  │
│   │   @endsection          │    │   @endsection          │                  │
│   │                        │    │                        │                  │
│   │   @section('content')  │    │   @section('content')  │                  │
│   │       @foreach         │    │       <form>           │                  │
│   │       @endforeach      │    │       </form>          │                  │
│   │   @endsection          │    │   @endsection          │                  │
│   │                        │    │                        │                  │
│   │   @push('styles')      │    │   @push('styles')      │                  │
│   │       user.css         │    │       form.css         │                  │
│   │   @endpush             │    │   @endpush             │                  │
│   └────────────────────────┘    └────────────────────────┘                  │
│                                                                             │
│   Result:                                                                   │
│   • Title filled by child                                                   │
│   • Content filled by child                                                 │
│   • Styles pushed from both children                                        │
│   • Scripts inherited from master                                           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Blade Templating

**Definition:** Blade is Laravel's powerful templating engine. Unlike other PHP templating engines, Blade does not restrict you from using plain PHP code in your views. All Blade views are compiled into plain PHP code and cached until they are modified, adding essentially zero overhead to your application.

Blade is Laravel's powerful templating engine.

```php
<?php
// routes/web.php
Route::get('/users', function () {
    return view('users.index', [
        'users' => User::all(),
        'title' => 'User List'
    ]);
});

// With compact()
Route::get('/users', function () {
    $users = User::all();
    return view('users.index', compact('users'));
});

// With view composer
data('title', 'User List');
return view('users.index');
```

**Basic Blade Syntax:**

```blade
{{-- resources/views/users/index.blade.php --}}

{{-- Echo variable (escaped by default) --}}
<h1>{{ $title }}</h1>

{{-- Echo unescaped HTML (use with caution!) --}}
<div>{!! $htmlContent !!}</div>

{{-- PHP code --}}
@php
    $count = count($users);
@endphp

{{-- Comments (not rendered in HTML) --}}
{{-- This is a Blade comment --}}

{{-- Include subview --}}
@include('partials.header')

{{-- Include with data --}}
@include('partials.user-card', ['user' => $user])

{{-- Conditional include --}}
@includeWhen($user->isAdmin(), 'partials.admin-menu')

{{-- Include if exists --}}
@includeIf('partials.optional')
```

### Template Inheritance

**Master Layout:**

```blade
{{-- resources/views/layouts/app.blade.php --}}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>@yield('title', 'My App')</title>
    @stack('styles')
</head>
<body>
    @include('partials.navigation')
    
    <main class="container">
        {{-- Main content section --}}
        @yield('content')
    </main>
    
    @include('partials.footer')
    
    {{-- Scripts section with default --}}
    @section('scripts')
        <script src="/js/app.js"></script>
    @show
    
    @stack('scripts')
</body>
</html>
```

**Child View:**

```blade
{{-- resources/views/users/index.blade.php --}}
@extends('layouts.app')

{{-- Override title section --}}
@section('title', 'Users - My App')

{{-- Push to styles stack --}}
@push('styles')
    <link rel="stylesheet" href="/css/users.css">
@endpush

{{-- Main content --}}
@section('content')
    <h1>All Users</h1>
    
    @if($users->isEmpty())
        <p>No users found.</p>
    @else
        <ul>
            @foreach($users as $user)
                <li>{{ $user->name }}</li>
            @endforeach
        </ul>
    @endif
@endsection

{{-- Extend scripts section --}}
@section('scripts')
    @parent {{-- Include parent scripts --}}
    <script src="/js/users.js"></script>
@endsection
```

### Control Structures

**Definition:** Blade provides convenient shortcuts for common PHP control structures, such as conditional statements and loops. These shortcuts provide a very clean, terse way of working with PHP control structures (`@if`, `@foreach`, `@auth`) while remaining familiar to their PHP counterparts.

```blade
{{-- If/Else --}}
@if($user->isAdmin())
    <span>Administrator</span>
@elseif($user->isModerator())
    <span>Moderator</span>
@else
    <span>User</span>
@endif

{{-- Unless (inverse of if) --}}
@unless($user->isAdmin())
    <p>You don't have admin access.</p>
@endunless

{{-- Authentication checks --}}
@auth
    <p>Welcome, {{ auth()->user()->name }}!</p>
@endauth

@guest
    <a href="/login">Login</a>
@endguest

{{-- Loops --}}
@foreach($users as $user)
    <p>{{ $user->name }}</p>
@endforeach

{{-- Loop with index --}}
@foreach($users as $index => $user)
    <p>{{ $index + 1 }}. {{ $user->name }}</p>
@endforeach

{{-- Forelse (empty check) --}}
@forelse($posts as $post)
    <article>{{ $post->title }}</article>
@empty
    <p>No posts available.</p>
@endforelse

{{-- While loop --}}
@while($condition)
    <p>Looping...</p>
@endwhile

{{-- For loop --}}
@for($i = 0; $i < 10; $i++)
    <p>Item {{ $i }}</p>
@endfor

{{-- Loop variable (available in loops) --}}
@foreach($users as $user)
    @if($loop->first)
        <p>First user: {{ $user->name }}</p>
    @endif
    
    <p>Index: {{ $loop->index }}</p>
    <p>Iteration: {{ $loop->iteration }}</p>
    <p>Remaining: {{ $loop->remaining }}</p>
    <p>Count: {{ $loop->count }}</p>
    <p>Even: {{ $loop->even }}</p>
    <p>Odd: {{ $loop->odd }}</p>
    
    @if($loop->last)
        <p>Last user: {{ $user->name }}</p>
    @endif
@endforeach

{{-- Break and continue --}}
@foreach($users as $user)
    @continue($user->isBanned())
    <p>{{ $user->name }}</p>
    @break($user->isAdmin())
@endforeach

{{-- Switch --}}
@switch($user->role)
    @case('admin')
        <span class="badge admin">Admin</span>
        @break
    @case('moderator')
        <span class="badge mod">Moderator</span>
        @break
    @default
        <span class="badge user">User</span>
@endswitch
```

### Blade Components

**Definition:** Components and slots provide similar benefits to sections and layouts; however, some may find the mental model of a component easier to understand. Components allow you to build reusable UI elements (like buttons, alerts, or cards) that can accept data and slots for content.

**Anonymous Components:**

```blade
{{-- resources/views/components/alert.blade.php --}}
@props(['type' => 'info', 'dismissible' => false])

<div {{ $attributes->merge(['class' => "alert alert-{$type}"]) }}>
    @if($dismissible)
        <button type="button" class="close">&times;</button>
    @endif
    
    {{ $slot }}
</div>
```

**Usage:**

```blade
<x-alert type="success" :dismissible="true" class="mt-4">
    Profile updated successfully!
</x-alert>
```

**Class-Based Components:**

```bash
php artisan make:component Alert
```

```php
<?php
// app/View/Components/Alert.php

namespace App\View\Components;

use Illuminate\View\Component;

class Alert extends Component
{
    public function __construct(
        public string $type = 'info',
        public bool $dismissible = false
    ) {}

    public function render(): View
    {
        return view('components.alert');
    }
}
```

**Named Slots:**

```blade
{{-- resources/views/components/card.blade.php --}}
<div class="card">
    @if(isset($header))
        <div class="card-header">
            {{ $header }}
        </div>
    @endif
    
    <div class="card-body">
        {{ $slot }}
    </div>
    
    @if(isset($footer))
        <div class="card-footer">
            {{ $footer }}
        </div>
    @endif
</div>
```

```blade
<x-card>
    <x-slot:header>
        <h3>Card Title</h3>
    </x-slot:header>
    
    <p>Card content goes here...</p>
    
    <x-slot:footer>
        <button>Action</button>
    </x-slot:footer>
</x-card>
```

**Inline Components:**

```bash
php artisan make:component Badge --inline
```

```php
<?php
// Single render method
public function render(): string
{
    return <<<'blade'
        <span class="badge bg-{{ $type }}">
            {{ $slot }}
        </span>
    blade;
}
```

### Blade Directives

**Definition:** Directives are custom shortcuts (starting with `@`) defined by Blade. Beyond built-in control structures, Laravel includes directives for authentication (`@auth`), environment checks (`@production`), and outputting JSON (`@json`). You can also define your own custom directives.

```blade
{{-- CSRF token --}}
<form method="POST" action="/profile">
    @csrf
    
    {{-- Method spoofing --}}
    @method('PUT')
    
    {{-- Old input --}}
    <input type="text" name="name" value="{{ old('name') }}">
    
    {{-- Error messages --}}
    @error('name')
        <span class="error">{{ $message }}</span>
    @enderror
</form>

{{-- Authentication --}}
@auth('admin')
    {{-- Admin content --}}
@endauth

@guest
    <a href="/login">Login</a>
@endguest

{{-- Environment --}}
@env('local')
    <div class="debug-banner">Debug Mode</div>
@endenv

@production
    {{-- Production-only analytics --}}
@endproduction

{{-- Localization --}}
@lang('messages.welcome')
@choice('messages.apples', $count)

{{-- JSON encoded data --}}
@json($array)
@json($array, JSON_PRETTY_PRINT)
```

---

## 6. Database & Migrations

> **Definition:** Migrations are version control for your database schema. They allow you to define database tables and columns in PHP code, enabling team collaboration, version control, and easy database schema evolution across different environments.

### Migration Workflow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        MIGRATION WORKFLOW                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              MIGRATION FILE STRUCTURE                            │     │
│   │                                                                  │     │
│   │   database/migrations/                                          │     │
│   │   └── 2024_01_01_000000_create_users_table.php                  │     │
│   │           │                                                     │     │
│   │           ▼                                                     │     │
│   │       ┌─────────────────┐                                       │     │
│   │       │   up()          │──▶ Create tables, columns, indexes   │     │
│   │       │   (Apply)       │                                       │     │
│   │       └─────────────────┘                                       │     │
│   │                                                                  │     │
│   │       ┌─────────────────┐                                       │     │
│   │       │   down()        │──▶ Reverse operations (drop)          │     │
│   │       │   (Rollback)    │                                       │     │
│   │       └─────────────────┘                                       │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              COMMAND WORKFLOW                                    │     │
│   │                                                                  │     │
│   │   Create          php artisan make:migration create_users_table │     │
│   │      │                                                          │     │
│   │      ▼                                                          │     │
│   │   Define          Write up() and down() methods                  │     │
│   │      │                                                          │     │
│   │      ▼                                                          │     │
│   │   Migrate         php artisan migrate ──▶ Run all pending        │     │
│   │      │                                     migrations           │     │
│   │      │                                                          │     │
│   │      ▼                                                          │     │
│   │   Rollback        php artisan migrate:rollback ──▶ Undo last    │     │
│   │      │                                           batch          │     │
│   │      │                                                          │     │
│   │      ▼                                                          │     │
│   │   Reset           php artisan migrate:reset ──▶ Undo all        │     │
│   │      │                                        migrations       │     │
│   │      │                                                          │     │
│   │      ▼                                                          │     │
│   │   Fresh           php artisan migrate:fresh ──▶ Drop all tables │     │
│   │                     and re-run migrations                       │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              SCHEMA BUILDER LIFECYCLE                            │     │
│   │                                                                  │     │
│   │   Schema::create('users', function (Blueprint $table) {          │     │
│   │       $table->id();           ──▶ Primary key                   │     │
│   │       $table->string('name'); ──▶ VARCHAR column                │     │
│   │       $table->text('bio');    ──▶ TEXT column                   │     │
│   │       $table->timestamps();   ──▶ created_at, updated_at        │     │
│   │       $table->softDeletes();  ──▶ deleted_at (soft delete)      │     │
│   │   });                                                            │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Migrations

**Definition:** Migrations are like version control for your database, allowing your team to define and share the application's database schema definition. They act as a blueprint for the database, allowing you to create tables and columns using PHP code rather than raw SQL.

Migrations are version control for your database schema.

```bash
# Create migration
php artisan make:migration create_users_table

# Create migration with specific table
php artisan make:migration add_votes_to_users_table --table=users

# Create migration and model
php artisan make:model Post -m

# Create migration, model, factory, seeder, and controller
php artisan make:model Post -mfsc

# Create migration with specific path
php artisan make:migration create_posts_table --path=database/migrations/tenant
```

**Creating Migrations:**

```php
<?php
// database/migrations/2024_01_01_000000_create_posts_table.php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('posts', function (Blueprint $table) {
            $table->id();  // Auto-incrementing primary key
            $table->foreignId('user_id')->constrained()->onDelete('cascade');
            $table->string('title');
            $table->string('slug')->unique();
            $table->text('content');
            $table->string('featured_image')->nullable();
            $table->enum('status', ['draft', 'published', 'archived'])->default('draft');
            $table->timestamp('published_at')->nullable();
            $table->timestamps();  // created_at and updated_at
            $table->softDeletes();  // deleted_at
            
            // Indexes
            $table->index('status');
            $table->index(['user_id', 'status']);
            $table->fullText('content');
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('posts');
    }
};
```

**Column Types:**

```php
<?php
$table->id();                           // Auto-incrementing UNSIGNED BIGINT
$table->foreignId('user_id');           // UNSIGNED BIGINT for foreign keys
$table->string('name');                 // VARCHAR(255)
$table->string('name', 100);            // VARCHAR(100)
$table->text('description');            // TEXT
$table->longText('content');            // LONGTEXT
$table->integer('votes');               // INTEGER
$table->bigInteger('votes');            // BIGINT
$table->smallInteger('level');          // SMALLINT
$table->tinyInteger('priority');        // TINYINT
$table->unsignedBigInteger('views');    // UNSIGNED BIGINT
$table->float('amount', 8, 2);          // FLOAT(8,2)
$table->double('amount', 15, 8);        // DOUBLE(15,8)
$table->decimal('amount', 10, 2);       // DECIMAL(10,2)
$table->boolean('is_active');           // BOOLEAN
$table->enum('status', ['a', 'b']);     // ENUM
$table->json('options');                // JSON
$table->jsonb('options');               // JSONB (PostgreSQL)
$table->date('birthday');               // DATE
$table->dateTime('created');            // DATETIME
$table->timestamp('added');             // TIMESTAMP
$table->timestamps();                   // created_at & updated_at
$table->softDeletes();                  // deleted_at
$table->timestampTz('added');           // TIMESTAMP with timezone
$table->time('sunrise');                // TIME
$table->timeTz('sunrise');              // TIME with timezone
$table->year('birth_year');             // YEAR
$table->binary('data');                 // BLOB
$table->uuid('id');                     // UUID
$table->ipAddress('visitor');           // IP address
$table->macAddress('device');           // MAC address
$table->geometry('coordinates');        // GEOMETRY
$table->point('position');              // POINT
$table->rememberToken();                // remember_token VARCHAR(100)
$table->nullableMorphs('taggable');     // taggable_id & taggable_type
```

**Column Modifiers:**

```php
<?php
$table->string('email')->unique();
$table->string('email')->index();
$table->string('email')->primary();
$table->integer('votes')->default(0);
$table->integer('votes')->nullable();
$table->integer('votes')->unsigned();
$table->string('name')->after('id');
$table->string('name')->first();
$table->string('name')->comment('User full name');
$table->timestamp('created_at')->useCurrent();
$table->timestamp('updated_at')->useCurrentOnUpdate();
$table->foreignId('user_id')->constrained();
```

### Running Migrations

```bash
# Run all pending migrations
php artisan migrate

# Rollback last batch of migrations
php artisan migrate:rollback

# Rollback all migrations
php artisan migrate:reset

# Rollback and re-run all migrations
php artisan migrate:refresh

# Drop all tables and re-run
php artisan migrate:fresh

# Refresh with seeders
php artisan migrate:fresh --seed

# Run specific migration file
php artisan migrate --path=database/migrations/2024_01_01_000000_create_users_table.php

# Show migration status
php artisan migrate:status
```

### Schema Builder

**Definition:** The Laravel `Schema` facade is a database agnostic way of manipulating tables. It allows you to create or modify database tables across any of Laravel's supported database systems using a unified, fluent API (e.g., `$table->string('email')->unique();`).

```php
<?php
use Illuminate\Support\Facades\Schema;

// Create table
Schema::create('users', function ($table) {
    $table->id();
    $table->string('name');
    $table->timestamps();
});

// Check if table exists
if (Schema::hasTable('users')) {
    // ...
}

// Check if column exists
if (Schema::hasColumn('users', 'email')) {
    // ...
}

// Rename table
Schema::rename($from, $to);

// Drop table
Schema::drop('users');
Schema::dropIfExists('users');

// Update existing table
Schema::table('users', function ($table) {
    $table->string('email');
});
```

**Modifying Columns:**

```php
<?php
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

Schema::table('users', function (Blueprint $table) {
    // Add column
    $table->string('nickname')->after('name');
    
    // Modify column (requires doctrine/dbal)
    $table->string('name', 100)->change();
    
    // Make nullable
    $table->string('nickname')->nullable()->change();
    
    // Rename column
    $table->renameColumn('from', 'to');
    
    // Drop column
    $table->dropColumn('nickname');
    
    // Drop multiple columns
    $table->dropColumn(['nickname', 'bio']);
    
    // Drop indexes
    $table->dropPrimary('users_id_primary');
    $table->dropUnique('users_email_unique');
    $table->dropIndex('geo_state_index');
    $table->dropForeign('users_user_id_foreign');
});
```

### Foreign Key Constraints

**Definition:** Foreign key constraints enforce referential integrity at the database level. Laravel provides a fluent syntax to define these constraints in migrations (e.g., `constrained()`), ensuring that relationships between tables (like posts belonging to users) are strictly maintained.

```php
<?php
Schema::table('posts', function (Blueprint $table) {
    // Simple foreign key
    $table->foreignId('user_id')
        ->constrained()
        ->onDelete('cascade');
    
    // With specific table
    $table->foreignId('user_id')
        ->constrained('users')
        ->onDelete('cascade');
    
    // Explicit foreign key definition
    $table->unsignedBigInteger('user_id');
    $table->foreign('user_id')
        ->references('id')
        ->on('users')
        ->onDelete('cascade')
        ->onUpdate('cascade');
});
```

### Seeders

**Definition:** Seeders allow you to populate your database with test data or initial settings data using seed classes. This is essential for setting up a development environment with realistic data or deploying required production data (like roles or countries) consistently.

```bash
# Create seeder
php artisan make:seeder UsersTableSeeder

# Create factory
php artisan make:factory PostFactory

# Run seeders
php artisan db:seed
php artisan db:seed --class=UsersTableSeeder
php artisan migrate:fresh --seed  # Refresh and seed
```

**Creating Seeders:**

```php
<?php
// database/seeders/DatabaseSeeder.php

namespace Database\Seeders;

use App\Models\User;
use App\Models\Post;
use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    public function run(): void
    {
        // Single user
        User::create([
            'name' => 'Admin User',
            'email' => 'admin@example.com',
            'password' => bcrypt('password'),
        ]);

        // Using factory
        User::factory(10)->create();
        
        // With relationships
        User::factory(5)
            ->has(Post::factory()->count(3))
            ->create();

        // Call other seeders
        $this->call([
            CategorySeeder::class,
            TagSeeder::class,
        ]);
    }
}
```

### Factories

**Definition:** Model factories define a blueprint for generating fake data for your Eloquent models. Powered by the Faker library, they allow you to easily create large volumes of test records (e.g., `User::factory()->count(50)->create()`) for testing and seeding.

```php
<?php
// database/factories/UserFactory.php

namespace Database\Factories;

use Illuminate\Database\Eloquent\Factories\Factory;
use Illuminate\Support\Str;

class UserFactory extends Factory
{
    protected $model = \App\Models\User::class;

    public function definition(): array
    {
        return [
            'name' => $this->faker->name(),
            'email' => $this->faker->unique()->safeEmail(),
            'email_verified_at' => now(),
            'password' => bcrypt('password'),
            'remember_token' => Str::random(10),
        ];
    }

    public function unverified(): static
    {
        return $this->state(fn (array $attributes) => [
            'email_verified_at' => null,
        ]);
    }

    public function admin(): static
    {
        return $this->state(fn (array $attributes) => [
            'role' => 'admin',
        ]);
    }
}
```

**Using Factories:**

```php
<?php
use App\Models\User;
use App\Models\Post;

// Create single
$user = User::factory()->create();

// Create multiple
$users = User::factory()->count(5)->create();

// Override attributes
$user = User::factory()->create([
    'name' => 'Custom Name',
]);

// Make (don't save)
$user = User::factory()->make();

// Use states
$user = User::factory()->unverified()->create();
$admin = User::factory()->admin()->create();

// Sequence for multiple
$users = User::factory()
    ->count(3)
    ->sequence(
        ['role' => 'admin'],
        ['role' => 'editor'],
        ['role' => 'user'],
    )
    ->create();

// With relationships
$posts = Post::factory()
    ->count(5)
    ->for(User::factory()->state([
        'name' => 'Author Name',
    ]))
    ->create();

// Many-to-many
$user = User::factory()
    ->hasAttached(
        Role::factory()->count(3),
        ['expires' => now()->addYear()]
    )
    ->create();
```

---

## 7. Eloquent ORM

> **Definition:** Eloquent is Laravel's ActiveRecord implementation for database operations. Each model represents a database table, allowing you to work with data using object-oriented syntax instead of writing raw SQL queries.

### Eloquent ORM Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        ELOQUENT ORM ARCHITECTURE                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │                      MODEL LAYER                                 │     │
│   │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │     │
│   │  │   Model      │  │   Builder    │  │  Collection  │           │     │
│   │  │   (Entity)   │  │   (Query)    │  │   (Results)  │           │     │
│   │  │              │  │              │  │              │           │     │
│   │  │ $fillable    │  │ where()      │  │ first()      │           │     │
│   │  │ $guarded     │  │ orWhere()    │  │ last()       │           │     │
│   │  │ $casts       │  │ orderBy()    │  │ map()        │           │     │
│   │  │ $hidden      │  │ with()       │  │ filter()     │           │     │
│   │  │ $appends     │  │ paginate()   │  │ pluck()      │           │     │
│   │  │ relationships│  │ get()        │  │ count()      │           │     │
│   │  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘           │     │
│   │         │                 │                 │                    │     │
│   │         └─────────────────┼─────────────────┘                    │     │
│   │                           ▼                                       │     │
│   │  ┌─────────────────────────────────────────────────────────────┐ │     │
│   │  │                    QUERY EXECUTION                          │ │     │
│   │  │                                                              │ │     │
│   │  │   User::where('active', true)    ──▶ Query Builder          │ │     │
│   │  │       ->orderBy('name')                                  │ │     │
│   │  │       ->with('posts')                                    │ │     │
│   │  │       ->get()              ──▶ Execute SQL                 │ │     │
│   │  │       │                                                  │ │     │
│   │  │       ▼                                                  │ │     │
│   │  │   Collection of User Models  ──▶ Hydrate Results           │ │     │
│   │  │                                                              │ │     │
│   │  └─────────────────────────────────────────────────────────────┘ │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              CRUD OPERATIONS FLOW                                │     │
│   │                                                                  │     │
│   │   CREATE    $user = User::create([...])                         │     │
│   │                  │                                               │     │
│   │                  ▼                                               │     │
│   │             INSERT INTO users (...) VALUES (...)                 │     │
│   │                                                                  │     │
│   │   READ      $user = User::find($id)                             │     │
│   │                  │                                               │     │
│   │                  ▼                                               │     │
│   │             SELECT * FROM users WHERE id = $id                   │     │
│   │                                                                  │     │
│   │   UPDATE    $user->update([...])                                │     │
│   │                  │                                               │     │
│   │                  ▼                                               │     │
│   │             UPDATE users SET ... WHERE id = $id                  │     │
│   │                                                                  │     │
│   │   DELETE    $user->delete()                                     │     │
│   │                  │                                               │     │
│   │                  ▼                                               │     │
│   │             DELETE FROM users WHERE id = $id                     │     │
│   │                  │                                               │     │
│   │                  └── Soft Delete: UPDATE deleted_at              │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Models

**Definition:** An Eloquent Model corresponds to a database table and allows you to interact with that table using an object-oriented syntax. Each database table has a corresponding "Model" used to interact with that table (e.g., `User` model for `users` table).

```bash
# Create model
php artisan make:model Post

# Create with migration, factory, seeder, controller
php artisan make:model Post -mfsc

# Create with resource controller
php artisan make:model Post -mfscr

# Create pivot model
php artisan make:model RoleUser --pivot
```

**Basic Model:**

```php
<?php
// app/Models/Post.php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\BelongsTo;
use Illuminate\Database\Eloquent\Relations\HasMany;
use Illuminate\Database\Eloquent\SoftDeletes;

class Post extends Model
{
    use HasFactory, SoftDeletes;

    // Table name (default: posts)
    protected $table = 'posts';

    // Primary key (default: id)
    protected $primaryKey = 'post_id';

    // Disable auto-increment
    public $incrementing = false;

    // Key type
    protected $keyType = 'string';

    // Disable timestamps
    public $timestamps = false;

    // Custom timestamp columns
    const CREATED_AT = 'creation_date';
    const UPDATED_AT = 'updated_date';

    // Database connection
    protected $connection = 'mysql';

    // Default values
    protected $attributes = [
        'status' => 'draft',
    ];

    // Mass assignable fields
    protected $fillable = [
        'user_id',
        'title',
        'slug',
        'content',
        'featured_image',
        'status',
        'published_at',
    ];

    // OR guarded (inverse of fillable)
    // protected $guarded = ['id', 'is_admin'];

    // Hidden from serialization
    protected $hidden = [
        'deleted_at',
    ];

    // Visible in serialization
    protected $visible = ['title', 'content'];

    // Append accessors to serialization
    protected $appends = ['excerpt'];

    // Type casting
    protected $casts = [
        'email_verified_at' => 'datetime',
        'published_at' => 'datetime',
        'is_published' => 'boolean',
        'metadata' => 'array',
        'options' => 'json',
        'settings' => 'object',
        'price' => 'decimal:2',
        'count' => 'integer',
        'views' => 'integer',
    ];

    // Relationships
    public function user(): BelongsTo
    {
        return $this->belongsTo(User::class);
    }

    public function comments(): HasMany
    {
        return $this->hasMany(Comment::class);
    }
}
```

### CRUD Operations

**Definition:** Eloquent makes CRUD (Create, Read, Update, Delete) operations intuitive. You use static methods on the model to create (`User::create()`) or retrieve records, and instance methods to update (`$user->save()`) or delete (`$user->delete()`) them.

```php
<?php
use App\Models\Post;

// Create
$post = Post::create([
    'title' => 'My Post',
    'content' => 'Post content',
]);

// Create and assign
$post = new Post;
$post->title = 'My Post';
$post->content = 'Post content';
$post->save();

// Mass assignment protection
$post = Post::make([
    'title' => 'My Post',
    'content' => 'Post content',
]);

// First or create
$post = Post::firstOrCreate(
    ['slug' => 'my-post'],
    ['title' => 'My Post', 'content' => 'Content']
);

// Update or create
$post = Post::updateOrCreate(
    ['slug' => 'my-post'],
    ['title' => 'Updated Title']
);

// First or new
$post = Post::firstOrNew(['slug' => 'my-post']);
$post->save();

// Read
$posts = Post::all();                    // All posts
$post = Post::find(1);                   // Find by id
$post = Post::findOrFail(1);             // Find or 404
$post = Post::first();                   // First post
$post = Post::firstOrFail();             // First or 404
$post = Post::find([1, 2, 3]);           // Find multiple

// With conditions
$posts = Post::where('status', 'published')->get();
$post = Post::where('slug', 'my-post')->first();

// Update
$post = Post::find(1);
$post->update(['title' => 'New Title']);

// Mass update
Post::where('status', 'draft')
    ->update(['status' => 'published']);

// Delete
$post = Post::find(1);
$post->delete();

// Delete by id
Post::destroy(1);
Post::destroy([1, 2, 3]);

// Mass delete
Post::where('status', 'archived')->delete();

// Soft delete
$post->delete();              // Soft delete
$post->forceDelete();         // Permanent delete
$post->restore();             // Restore soft-deleted

// Trashed models
Post::withTrashed()->get();
Post::onlyTrashed()->get();
```

### Mass Assignment ($fillable vs $guarded)

**Definition:** Mass assignment creates or updates a model from an array of attributes (like `Request::all()`). To prevent security vulnerabilities (users changing protected columns like `is_admin`), Eloquent requires you to whitelist allow attributes in `$fillable` or blacklist them in `$guarded`.

```php
<?php
// Using $fillable (whitelist approach - RECOMMENDED)
class Post extends Model
{
    protected $fillable = [
        'title',
        'content',
        'published_at',
    ];
}

// Using $guarded (blacklist approach)
class Post extends Model
{
    protected $guarded = [
        'id',
        'is_admin',
        'password',
    ];

    // Guard everything (disable mass assignment)
    protected $guarded = ['*'];

    // Guard nothing (allow everything - DANGEROUS!)
    protected $guarded = [];
}

// Best practice: Use $fillable with specific fields
```

### Query Scopes

**Definition:** Query scopes allow you to define common sets of query constraints that you may easily reuse throughout your application. For example, you might define a `scopeActive` to only retrieve users that are active (`User::active()->get()`).

```php
<?php
class Post extends Model
{
    // Local scope
    public function scopePublished($query)
    {
        return $query->where('status', 'published');
    }

    public function scopeOfCategory($query, $categoryId)
    {
        return $query->where('category_id', $categoryId);
    }

    public function scopeRecent($query, $days = 7)
    {
        return $query->where('created_at', '>=', now()->subDays($days));
    }

    // Dynamic scope
    public function scopeStatus($query, $status)
    {
        return $query->where('status', $status);
    }

    // Global scope
    protected static function booted(): void
    {
        static::addGlobalScope('published', function ($query) {
            $query->where('status', 'published');
        });
    }
}

// Usage
$posts = Post::published()->get();
$posts = Post::ofCategory(5)->get();
$posts = Post::recent(30)->get();
$posts = Post::status('draft')->get();

// Chaining
$posts = Post::published()
    ->ofCategory(5)
    ->recent()
    ->get();

// Remove global scope
$posts = Post::withoutGlobalScope('published')->get();
$posts = Post::withoutGlobalScopes()->get();
```

### Accessors & Mutators

**Definition:** **Accessors** transform an Eloquent attribute value when it is accessed (e.g., formatting a date). **Mutators** transform an attribute value when it is set (e.g., hashing a password). They allow you to format data transparently between the database and the application.

```php
<?php
class User extends Model
{
    // Accessor (get)
    protected function firstName(): Attribute
    {
        return Attribute::make(
            get: fn (string $value) => ucfirst($value),
        );
    }

    // Mutator (set)
    protected function password(): Attribute
    {
        return Attribute::make(
            set: fn (string $value) => bcrypt($value),
        );
    }

    // Combined
    protected function name(): Attribute
    {
        return Attribute::make(
            get: fn (string $value) => ucwords($value),
            set: fn (string $value) => strtolower($value),
        );
    }

    // Accessor with caching
    protected function fullName(): Attribute
    {
        return Attribute::make(
            get: function (mixed $value, array $attributes) {
                return $attributes['first_name'] . ' ' . $attributes['last_name'];
            },
        );
    }

    // Mutator with additional attributes
    protected function address(): Attribute
    {
        return Attribute::make(
            set: function (array $value) {
                return [
                    'address_line_1' => $value['line1'],
                    'address_line_2' => $value['line2'] ?? null,
                    'city' => $value['city'],
                    'postal_code' => $value['postal'],
                ];
            },
        );
    }
}
```

### Collections

**Definition:** The `Illuminate\Support\Collection` class provides a fluent, convenient wrapper for working with arrays of data. Eloquent returns multiple results as a Collection instance, giving you access to powerful methods like `map`, `filter`, `reduce`, and `pluck`.

```php
<?php
$posts = Post::all();

// Filtering
$published = $posts->where('status', 'published');
$recent = $posts->where('created_at', '>=', now()->subWeek());

// Transforming
$titles = $posts->pluck('title');
$mapped = $posts->map(function ($post) {
    return [
        'id' => $post->id,
        'title' => $post->title,
    ];
});

// Aggregations
$count = $posts->count();
$max = $posts->max('views');
$avg = $posts->avg('rating');
$sum = $posts->sum('views');

// Sorting
$sorted = $posts->sortBy('title');
$sorted = $posts->sortByDesc('views');

// Grouping
$byStatus = $posts->groupBy('status');

// First/Last
$first = $posts->first();
$last = $posts->last();

// Checking
$hasPublished = $posts->contains('status', 'published');
$allPublished = $posts->every('status', 'published');

// Chunking
$posts->chunk(100)->each(function ($chunk) {
    // Process 100 posts at a time
});

// Higher-order messages
$posts->each->update(['status' => 'published']);
$titles = $posts->map->title;
```

### Pagination

**Definition:** Laravel's paginator integrates with the query builder and Eloquent ORM to provide convenient, easy-to-use pagination of database results out of the box. By calling `paginate()`, Laravel automatically limits results and generates the necessary HTML links for the UI.

```php
<?php
// Simple pagination (faster for large datasets)
$posts = Post::paginate(15);

// Cursor pagination (for very large datasets)
$posts = Post::cursorPaginate(15);

// With query string preservation
$posts = Post::paginate(15)->withQueryString();

// Custom path
$posts = Post::paginate(15)->withPath('/custom/url');

// Append parameters
$posts = Post::paginate(15)->appends(['sort' => 'name']);

// Fragment anchor
$posts = Post::paginate(15)->fragment('posts');

// In view
// resources/views/posts/index.blade.php
@foreach($posts as $post)
    <p>{{ $post->title }}</p>
@endforeach

{{ $posts->links() }}

{{-- Custom pagination view --}}
{{ $posts->links('vendor.pagination.custom') }}

{{-- Simple pagination (Previous/Next only) --}}
{{ $posts->links('pagination::simple-bootstrap-5') }}
```

---

## 8. Eloquent Relationships

> **Definition:** Eloquent relationships define how models connect to each other, mapping database table associations to object-oriented methods. Laravel provides six relationship types to model real-world data associations.

### Relationship Types

### Relationship Types Reference

| Type | Description | Inverse |
|------|-------------|---------|
| **One to One** | A single record related to another single record | `hasOne` / `belongsTo` |
| **One to Many** | A single record related to multiple records | `hasMany` / `belongsTo` |
| **Many to Many** | Multiple records related to multiple records (needs pivot table) | `belongsToMany` |
| **Has One Through** | Relates models via an intermediate model (single) | `hasOneThrough` |
| **Has Many Through** | Relates models via an intermediate model (multiple) | `hasManyThrough` |
| **Polymorphic** | A model can belong to more than one other model type | `morphTo` / `morphOne` / `morphMany` |

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      ELOQUENT RELATIONSHIP TYPES                            │

├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │  1. ONE-TO-ONE                                                   │     │
│   │                                                                  │     │
│   │     User ────────────────▶ Profile                               │     │
│   │     hasOne()              belongsTo()                           │     │
│   │                                                                  │     │
│   │     users table              profiles table                      │     │
│   │     id                       id                                  │     │
│   │     name                     user_id (FK)                        │     │
│   │                              bio                                 │     │
│   │                                                                  │     │
│   ├──────────────────────────────────────────────────────────────────┤     │
│   │  2. ONE-TO-MANY                                                  │     │
│   │                                                                  │     │
│   │     User ────────────────▶ Posts (many)                          │     │
│   │     hasMany()             belongsTo()                           │     │
│   │                                                                  │     │
│   │     users table              posts table                         │     │
│   │     id                       id                                  │     │
│   │     name                     user_id (FK)                        │     │
│   │                              title                               │     │
│   │                                                                  │     │
│   ├──────────────────────────────────────────────────────────────────┤     │
│   │  3. MANY-TO-MANY                                                 │     │
│   │                                                                  │     │
│   │     User ◀────────────▶ Roles (pivot table)                      │     │
│   │     belongsToMany()     belongsToMany()                          │     │
│   │                                                                  │     │
│   │     users    role_user    roles                                  │     │
│   │     ─────    ─────────    ─────                                  │     │
│   │     id       user_id      id                                     │     │
│   │     name     role_id      name                                   │     │
│   │                                                                  │     │
│   ├──────────────────────────────────────────────────────────────────┤     │
│   │  4. HAS ONE THROUGH                                              │     │
│   │                                                                  │     │
│   │     Mechanic ─────▶ Car ─────▶ Owner                             │     │
│   │     hasOneThrough()                                            │     │
│   │                                                                  │     │
│   │     mechanics    cars        car_owners                          │     │
│   │     ─────────    ────        ──────────                          │     │
│   │     id           id          id                                  │     │
│   │     name         mechanic_id car_id                              │     │
│   │                                                                  │     │
│   ├──────────────────────────────────────────────────────────────────┤     │
│   │  5. HAS MANY THROUGH                                             │     │
│   │                                                                  │     │
│   │     Country ─────▶ Users ─────▶ Posts                            │     │
│   │     hasManyThrough()                                           │     │
│   │                                                                  │     │
│   │     countries    users       posts                               │     │
│   │     ─────────    ─────       ─────                               │     │
│   │     id           id          id                                  │     │
│   │     name         country_id  user_id                             │     │
│   │                                                                  │     │
│   ├──────────────────────────────────────────────────────────────────┤     │
│   │  6. POLYMORPHIC                                                  │     │
│   │                                                                  │     │
│   │     Post ───┐                                                    │     │
│   │               ├──▶ Comments (commentable)                        │     │
│   │     Video ──┘                                                    │     │
│   │     morphMany()    morphTo()                                     │     │
│   │                                                                  │     │
│   │     comments table                                               │     │
│   │     ────────────────                                             │     │
│   │     id                                                           │     │
│   │     body                                                         │     │
│   │     commentable_id      (post_id or video_id)                    │     │
│   │     commentable_type    ('App\Models\Post' or 'Video')           │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              EAGER LOADING VS LAZY LOADING                       │     │
│   │                                                                  │     │
│   │   LAZY (N+1 Problem)          EAGER (Optimized)                  │     │
│   │   ─────────────────           ─────────────────                  │     │
│   │   $users = User::all();       $users = User::with('posts')       │     │
│   │   foreach ($users as $user)       ->get();                       │     │
│   │       $user->posts;   ◄──▶    foreach ($users as $user)          │     │
│   │   │   // Query for each            $user->posts;   ◄── Cached    │     │
│   │   │   // N queries + 1             // 2 queries total            │     │
│   │   │                                                            │     │
│   │   └── 1 query for users                                        │     │
│   │       + N queries for posts                                    │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### One-to-One

```php
<?php
class User extends Model
{
    // User has one profile
    public function profile(): HasOne
    {
        return $this->hasOne(Profile::class);
    }
}

class Profile extends Model
{
    // Profile belongs to user
    public function user(): BelongsTo
    {
        return $this->belongsTo(User::class);
    }
}

// Usage
$user = User::find(1);
$profile = $user->profile;
$user = $profile->user;

// With custom foreign key
public function profile(): HasOne
{
    return $this->hasOne(Profile::class, 'user_id', 'id');
}

// Inverse with custom key
public function user(): BelongsTo
{
    return $this->belongsTo(User::class, 'user_id', 'id');
}
```

### One-to-Many

```php
<?php
class User extends Model
{
    // User has many posts
    public function posts(): HasMany
    {
        return $this->hasMany(Post::class);
    }
}

class Post extends Model
{
    // Post belongs to user
    public function user(): BelongsTo
    {
        return $this->belongsTo(User::class);
    }
}

// Usage
$user = User::find(1);
$posts = $user->posts;

// Create with relationship
$user->posts()->create([
    'title' => 'New Post',
    'content' => 'Content',
]);

// Associate existing
$post->user()->associate($user);
$post->save();

// Dissociate
$post->user()->dissociate();
$post->save();

// Count
$postCount = $user->posts()->count();

// Query relationship
$recentPosts = $user->posts()
    ->where('created_at', '>=', now()->subWeek())
    ->get();
```

### Many-to-Many

```php
<?php
class User extends Model
{
    // User belongs to many roles
    public function roles(): BelongsToMany
    {
        return $this->belongsToMany(Role::class);
    }

    // With pivot table attributes
    public function roles(): BelongsToMany
    {
        return $this->belongsToMany(Role::class)
            ->withPivot('expires_at', 'is_active')
            ->withTimestamps();
    }

    // Custom table and keys
    public function roles(): BelongsToMany
    {
        return $this->belongsToMany(
            Role::class,
            'role_user',      // Pivot table
            'user_id',        // Foreign key on pivot
            'role_id'         // Related key on pivot
        );
    }
}

class Role extends Model
{
    public function users(): BelongsToMany
    {
        return $this->belongsToMany(User::class);
    }
}

// Usage
$user = User::find(1);
$roles = $user->roles;

// Attach
$user->roles()->attach($roleId);
$user->roles()->attach([1, 2, 3]);
$user->roles()->attach($roleId, ['expires_at' => now()->addYear()]);

// Detach
$user->roles()->detach($roleId);
$user->roles()->detach([1, 2]);
$user->roles()->detach(); // Detach all

// Sync (detach all then attach)
$user->roles()->sync([1, 2, 3]);
$user->roles()->syncWithoutDetaching([4, 5]); // Don't detach existing

// Toggle
$user->roles()->toggle([1, 2, 3]);

// Update existing pivot
$user->roles()->updateExistingPivot($roleId, [
    'expires_at' => now()->addYear(),
]);

// Access pivot data
foreach ($user->roles as $role) {
    echo $role->pivot->expires_at;
    echo $role->pivot->created_at;
}
```

### Eager Loading

```php
<?php
// N+1 problem (AVOID!)
$users = User::all();
foreach ($users as $user) {
    echo $user->profile->bio; // Queries profile for each user
}

// Eager loading (GOOD!)
$users = User::with('profile')->get();
foreach ($users as $user) {
    echo $user->profile->bio; // Already loaded
}

// Multiple relationships
$users = User::with(['profile', 'posts', 'roles'])->get();

// Nested relationships
$users = User::with('posts.comments')->get();

// Eager load with constraints
$users = User::with(['posts' => function ($query) {
    $query->where('status', 'published');
}])->get();

// Load after query (lazy eager loading)
$users = User::all();
$users->load('profile');
$users->loadMissing('posts'); // Only if not loaded

// Load specific relationships
$users->load(['posts' => function ($query) {
    $query->where('created_at', '>=', now()->subWeek());
}]);

// Count eager loading
$users = User::withCount('posts')->get();
echo $users[0]->posts_count;

// With condition
$users = User::withCount(['posts' => function ($query) {
    $query->where('status', 'published');
}])->get();
```

### Polymorphic Relations

**One-to-Many Polymorphic:**

```php
<?php
// comments table: id, body, commentable_id, commentable_type

class Comment extends Model
{
    public function commentable(): MorphTo
    {
        return $this->morphTo();
    }
}

class Post extends Model
{
    public function comments(): MorphMany
    {
        return $this->morphMany(Comment::class, 'commentable');
    }
}

class Video extends Model
{
    public function comments(): MorphMany
    {
        return $this->morphMany(Comment::class, 'commentable');
    }
}

// Usage
$post = Post::find(1);
$comments = $post->comments;

$comment = new Comment(['body' => 'Great post!']);
$post->comments()->save($comment);
```

**Many-to-Many Polymorphic:**

```php
<?php
// tags table: id, name
// taggables table: tag_id, taggable_id, taggable_type

class Tag extends Model
{
    public function posts(): MorphToMany
    {
        return $this->morphedByMany(Post::class, 'taggable');
    }

    public function videos(): MorphToMany
    {
        return $this->morphedByMany(Video::class, 'taggable');
    }
}

class Post extends Model
{
    public function tags(): MorphToMany
    {
        return $this->morphToMany(Tag::class, 'taggable');
    }
}

// Usage
$post->tags()->attach($tagId);
$post->tags()->sync([1, 2, 3]);
```

**Polymorphic One-to-One:**

```php
<?php
class User extends Model
{
    public function image(): MorphOne
    {
        return $this->morphOne(Image::class, 'imageable');
    }
}

class Post extends Model
{
    public function image(): MorphOne
    {
        return $this->morphOne(Image::class, 'imageable');
    }
}

class Image extends Model
{
    public function imageable(): MorphTo
    {
        return $this->morphTo();
    }
}
```

### Has Many Through

```php
<?php
// Country -> Users -> Posts
// countries -> id, name
// users -> id, country_id, name
// posts -> id, user_id, title

class Country extends Model
{
    public function posts(): HasManyThrough
    {
        return $this->hasManyThrough(Post::class, User::class);
    }

    // Custom keys
    public function posts(): HasManyThrough
    {
        return $this->hasManyThrough(
            Post::class,
            User::class,
            'country_id', // Foreign key on users table
            'user_id',    // Foreign key on posts table
            'id',         // Local key on countries table
            'id'          // Local key on users table
        );
    }
}

// Usage
$country = Country::find(1);
$posts = $country->posts;
```

### Has One Through

```php
<?php
// Mechanic -> Car -> Owner
// mechanics -> id, name
// cars -> id, mechanic_id, model
// car_owners -> id, car_id, name

class Mechanic extends Model
{
    public function carOwner(): HasOneThrough
    {
        return $this->hasOneThrough(
            CarOwner::class,
            Car::class,
            'mechanic_id', // Foreign key on cars table
            'car_id',      // Foreign key on owners table
            'id',          // Local key on mechanics table
            'id'           // Local key on cars table
        );
    }
}
```

---

## 9. Request & Validation

> **Definition:** Laravel's Request object encapsulates HTTP request data (input, files, headers), while the Validation system ensures data integrity by checking input against defined rules before processing.

### Validation Flow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        VALIDATION FLOW                                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │                   REQUEST LIFECYCLE                              │     │
│   │                                                                  │     │
│   │   HTTP Request ──▶ Route ──▶ Controller/Form Request            │     │
│   │                                      │                          │     │
│   │                                      ▼                          │     │
│   │                              ┌──────────────┐                   │     │
│   │                              │  Validation  │                   │     │
│   │                              │   Rules      │                   │     │
│   │                              └──────┬───────┘                   │     │
│   │                                     │                           │     │
│   │                    ┌────────────────┴────────────────┐          │     │
│   │                    ▼                                 ▼          │     │
│   │            ┌──────────────┐                 ┌──────────────┐    │     │
│   │            │  VALID       │                 │  INVALID     │    │     │
│   │            │              │                 │              │    │     │
│   │            │ Return       │                 │ Throw        │    │     │
│   │            │ validated    │                 │ Validation   │    │     │
│   │            │ data         │                 │ Exception    │    │     │
│   │            └──────┬───────┘                 └──────┬───────┘    │     │
│   │                   │                                │             │     │
│   │                   ▼                                ▼             │     │
│   │            ┌──────────────┐                 ┌──────────────┐    │     │
│   │            │  Process     │                 │  Redirect    │    │     │
│   │            │  Request     │                 │  with Errors │    │     │
│   │            └──────────────┘                 └──────────────┘    │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              VALIDATION RULE HIERARCHY                           │     │
│   │                                                                  │     │
│   │   Field Rules                                                    │     │
│   │   ├── required        Must be present and not empty             │     │
│   │   ├── nullable        Can be null or missing                    │     │
│   │   ├── sometimes       Only validate if present                  │     │
│   │                                                                  │     │
│   │   Type Rules                                                     │     │
│   │   ├── string          Must be string                            │     │
│   │   ├── integer         Must be integer                           │     │
│   │   ├── numeric         Must be numeric                           │     │
│   │   ├── boolean         Must be boolean                           │     │
│   │   ├── array           Must be array                             │     │
│   │   ├── date            Must be valid date                        │     │
│   │                                                                  │     │
│   │   Format Rules                                                   │     │
│   │   ├── email           Valid email format                        │     │
│   │   ├── url             Valid URL                                 │     │
│   │   ├── regex:pattern   Matches regex                             │     │
│   │   ├── min:value       Minimum length/value                      │     │
│   │   ├── max:value       Maximum length/value                      │     │
│   │                                                                  │     │
│   │   Database Rules                                                 │     │
│   │   ├── unique:table    Must be unique                            │     │
│   │   └── exists:table    Must exist in database                    │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              FORM REQUEST LIFECYCLE                              │     │
│   │                                                                  │     │
│   │   1. authorize() ──▶ Check user can make this request            │     │
│   │          │                                                       │     │
│   │          ▼                                                       │     │
│   │   2. prepareForValidation() ──▶ Modify input before validation   │     │
│   │          │                                                       │     │
│   │          ▼                                                       │     │
│   │   3. rules() ──▶ Define validation rules                         │     │
│   │          │                                                       │     │
│   │          ▼                                                       │     │
│   │   4. Validation executes                                         │     │
│   │          │                                                       │     │
│   │          ▼                                                       │     │
│   │   5. passedValidation() ──▶ Modify validated data                │     │
│   │          │                                                       │     │
│   │          ▼                                                       │     │
│   │   6. Return validated data to controller                         │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Accessing Request Data

**Definition:** The `Illuminate\Http\Request` instance provides an object-oriented way to interact with the current HTTP request. It allows you to retrieve input data, uploaded files, cookies, and headers, as well as inspect the request method and path.

```php
<?php
namespace App\Http\Controllers;

use Illuminate\Http\Request;

class UserController extends Controller
{
    public function store(Request $request)
    {
        // All input
        $all = $request->all();

        // Specific input
        $name = $request->input('name');
        $name = $request->input('name', 'default');
        $name = $request->name;  // Magic property

        // Nested input
        $city = $request->input('address.city');

        // Array input
        $names = $request->input('products.0.name');
        $names = $request->input('products.*.name');

        // Query string only
        $search = $request->query('search');

        // Only specific fields
        $input = $request->only(['name', 'email']);
        $input = $request->only('name', 'email');

        // Except specific fields
        $input = $request->except(['password', '_token']);

        // Has/Has Any/Missing
        if ($request->has('name')) { }
        if ($request->hasAny(['name', 'email'])) { }
        if ($request->missing('name')) { }
        if ($request->filled('name')) { }

        // Boolean input (checkboxes)
        $agree = $request->boolean('agree');

        // Date input
        $birthday = $request->date('birthday');
        $birthday = $request->date('birthday', 'Y-m-d', 'Europe/Paris');

        // Collect input
        $names = $request->collect('names');

        // String input
        $name = $request->string('name')->trim()->lower();

        // Enum input
        $status = $request->enum('status', Status::class);

        // File upload
        $file = $request->file('avatar');
        $file = $request->avatar;  // Magic property

        // Request info
        $method = $request->method();
        $url = $request->url();
        $fullUrl = $request->fullUrl();
        $path = $request->path();
        $ip = $request->ip();
        $userAgent = $request->userAgent();

        // Headers
        $token = $request->header('X-Token');
        $bearerToken = $request->bearerToken();
    }
}
```

### Validation Rules

**Definition:** Laravel provides a vast library of built-in validation rules (e.g., `required`, `email`, `unique`, `min`, `max`) that can be applied to incoming data. These rules are defined as an array or a pipe-delimited string and passed to the `validate` method.

```php
<?php
public function store(Request $request)
{
    $validated = $request->validate([
        // Required
        'name' => 'required',
        'email' => 'required|email',
        'password' => 'required|min:8',

        // String validation
        'name' => 'required|string|max:255',
        'bio' => 'nullable|string|min:10|max:1000',

        // Email
        'email' => 'required|email|unique:users,email',
        'email' => 'required|email:rfc,dns',  // Validate DNS

        // Numeric
        'age' => 'required|integer|min:18|max:120',
        'price' => 'required|numeric|min:0|max:9999.99',
        'rating' => 'required|decimal:0,2',

        // Boolean
        'subscribe' => 'boolean',

        // Date
        'birthday' => 'required|date',
        'birthday' => 'required|date_format:Y-m-d',
        'start_date' => 'required|date|after_or_equal:today',
        'end_date' => 'required|date|after:start_date',

        // File upload
        'avatar' => 'required|image|mimes:jpg,png|max:2048',
        'document' => 'required|file|mimes:pdf,docx|max:5120',

        // Array
        'tags' => 'required|array',
        'tags.*' => 'required|string|max:50',  // Each tag

        // In/Not In
        'status' => 'required|in:active,inactive,pending',
        'role' => 'required|not_in:admin,superadmin',

        // Regex
        'phone' => 'required|regex:/^[0-9]{10}$/',

        // Exists/Unique
        'user_id' => 'required|exists:users,id',
        'email' => 'required|email|unique:users,email',
        'email' => 'required|email|unique:users,email,' . $userId,  // Ignore user

        // Confirmed (password_confirmation field)
        'password' => 'required|min:8|confirmed',

        // Same/Different
        'password' => 'required|same:password_confirmation',
        'new_email' => 'required|email|different:old_email',

        // Conditional rules
        'company_name' => 'required_if:type,company',
        'tax_id' => 'required_unless:type,individual',
        'spouse_name' => 'required_with:marital_status',

        // Custom messages
    ], [
        'email.required' => 'Please provide your email address.',
        'email.email' => 'The email must be a valid address.',
        'password.min' => 'Password must be at least :min characters.',
    ]);

    // Validation passed, use $validated
}
```

**Common Validation Rules:**

| Rule | Description |
|------|-------------|
| `required` | Must be present and not empty |
| `nullable` | Can be null |
| `string` | Must be a string |
| `email` | Valid email format |
| `url` | Valid URL |
| `ip` | Valid IP address |
| `json` | Valid JSON string |
| `uuid` | Valid UUID |
| `alpha` | Only alphabetic characters |
| `alpha_num` | Alphanumeric characters |
| `alpha_dash` | Alphanumeric, dash, underscore |
| `numeric` | Must be numeric |
| `integer` | Must be integer |
| `boolean` | Must be boolean |
| `date` | Valid date |
| `date_format:format` | Match date format |
| `after:date` | Date after given date |
| `before:date` | Date before given date |
| `min:value` | Minimum value/length |
| `max:value` | Maximum value/length |
| `size:value` | Exact size |
| `between:min,max` | Between min and max |
| `confirmed` | Must have matching _confirmation field |
| `unique:table,column` | Must be unique in database |
| `exists:table,column` | Must exist in database |
| `distinct` | No duplicates in array |
| `filled` | Must not be empty when present |
| `present` | Must be present (can be empty) |
| `prohibited` | Must not be present |
| `required_if:field,value` | Required if another field equals value |
| `required_with:foo,bar` | Required if any of fields are present |
| `regex:pattern` | Must match regex pattern |
| `file` | Must be uploaded file |
| `image` | Must be image (jpeg, png, bmp, gif, svg, webp) |
| `mimes:jpg,png` | Allowed file extensions |
| `mimetypes:image/jpeg` | Allowed MIME types |
| `dimensions:min_width=100` | Image dimension rules |

### Form Requests

**Definition:** Form Requests are custom request classes that encapsulate validation and authorization logic for a specific action. Moving this logic out of controllers and into dedicated classes keeps code clean, reusable, and ensures validation is performed automatically before the controller method is even called.

```bash
php artisan make:request StoreUserRequest
```

```php
<?php
// app/Http/Requests/StoreUserRequest.php

namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;
use Illuminate\Validation\Rule;
use Illuminate\Validation\Rules\Password;

class StoreUserRequest extends FormRequest
{
    // Authorize the request
    public function authorize(): bool
    {
        return auth()->check() && auth()->user()->isAdmin();
    }

    // Validation rules
    public function rules(): array
    {
        return [
            'name' => ['required', 'string', 'max:255'],
            'email' => [
                'required',
                'email',
                Rule::unique('users', 'email'),
            ],
            'password' => [
                'required',
                Password::min(8)
                    ->letters()
                    ->mixedCase()
                    ->numbers()
                    ->symbols()
                    ->uncompromised(),
            ],
            'role' => ['required', Rule::in(['user', 'editor', 'admin'])],
            'avatar' => ['nullable', 'image', 'max:2048'],
        ];
    }

    // Custom messages
    public function messages(): array
    {
        return [
            'name.required' => 'Please enter your name.',
            'email.unique' => 'This email is already registered.',
        ];
    }

    // Custom attributes
    public function attributes(): array
    {
        return [
            'name' => 'full name',
            'email' => 'email address',
        ];
    }

    // Prepare data before validation
    protected function prepareForValidation(): void
    {
        $this->merge([
            'slug' => Str::slug($this->name),
        ]);
    }

    // After validation hook
    protected function passedValidation(): void
    {
        $this->merge([
            'password' => bcrypt($this->password),
        ]);
    }
}
```

**Using Form Request:**

```php
<?php
use App\Http\Requests\StoreUserRequest;

class UserController extends Controller
{
    public function store(StoreUserRequest $request)
    {
        // Validation passed
        $validated = $request->validated();
        
        // Or specific fields
        $safe = $request->safe()->only(['name', 'email']);
        
        User::create($validated);
        
        return redirect()->route('users.index');
    }
}
```

### Error Messages

**Definition:** When validation fails, Laravel automatically redirects the user back to the previous location with error messages flashed to the session. You can customize these messages globally in language files or per-request to provide clear feedback to users.

```php
<?php
// In controller
public function store(Request $request)
{
    $validator = Validator::make($request->all(), [
        'name' => 'required',
        'email' => 'required|email',
    ]);

    if ($validator->fails()) {
        return redirect('register')
            ->withErrors($validator)
            ->withInput();
    }

    // Or throw ValidationException
    $validated = $validator->validate();
}
```

**Displaying Errors:**

```blade
{{-- Display all errors --}}
@if($errors->any())
    <div class="alert alert-danger">
        <ul>
            @foreach($errors->all() as $error)
                <li>{{ $error }}</li>
            @endforeach
        </ul>
    </div>
@endif

{{-- Display specific error --}}
@error('email')
    <span class="text-danger">{{ $message }}</span>
@enderror

{{-- Check for specific error --}}
@if($errors->has('email'))
    <span>Please fix the email field.</span>
@endif

{{-- First error --}}
<span>{{ $errors->first('email') }}</span>

{{-- Old input --}}
<input type="email" name="email" value="{{ old('email') }}">
```

---

## 10. Middleware

> **Definition:** Middleware provides a mechanism to filter HTTP requests entering your application. It acts as a bridge between the request and response, allowing you to perform operations before and after the request is handled.

### Middleware Pipeline

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        MIDDLEWARE PIPELINE                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              REQUEST FLOW THROUGH MIDDLEWARE                     │     │
│   │                                                                  │     │
│   │   HTTP Request                                                   │     │
│   │        │                                                         │     │
│   │        ▼                                                         │     │
│   │   ┌─────────────────┐                                            │     │
│   │   │ Global          │  ┌─────────────────────────────────────┐  │     │
│   │   │ Middleware      │  │ (TrustProxies, HandleCors, etc.)    │  │     │
│   │   └────────┬────────┘  └─────────────────────────────────────┘  │     │
│   │            │                                                    │     │
│   │            ▼                                                    │     │
│   │   ┌─────────────────┐     ┌─────────────────────────────────────┐     │
│   │   │ Route Specific  │     │ (auth, verified, role:admin, etc.)  │     │
│   │   │ Middleware      │     └─────────────────────────────────────┘     │
│   │   └────────┬────────┘                                            │     │
│   │            │                                                     │     │
│   │            ▼                                                     │     │
│   │   ┌─────────────────┐                                            │     │
│   │   │ Controller      │  Process Request                            │     │
│   │   │ Execute         │                                            │     │
│   │   └────────┬────────┘                                            │     │
│   │            │                                                     │     │
│   │            ▼                                                     │     │
│   │   ┌─────────────────┐     ┌─────────────────────────────────────┐     │
│   │   │ Response        │     │ (Modify headers, cookies, etc.)     │     │
│   │   │ Middleware      │     └─────────────────────────────────────┘     │
│   │   └────────┬────────┘                                            │     │
│   │            │                                                     │     │
│   │            ▼                                                     │     │
│   │   ┌─────────────────┐     ┌─────────────────────────────────────┐     │
│   │   │ Global          │     │ (Final processing)                  │     │
│   │   │ Terminable      │     └─────────────────────────────────────┘     │     │
│   │   └────────┬────────┘                                            │     │
│   │            │                                                     │     │
│   │            ▼                                                     │     │
│   │   HTTP Response                                                  │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              MIDDLEWARE TYPES                                    │     │
│   │                                                                  │     │
│   │   BEFORE MIDDLEWARE              AFTER MIDDLEWARE                │     │
│   │   ───────────────────            ────────────────                │     │
│   │   public function handle()       public function handle()        │     │
│   │   {                              {                               │     │
│   │       // Check request               $response = $next($request);│     │
│   │       if (!condition) {              // Modify response          │     │
│   │           return abort(403);         $response->header(...);     │     │
│   │       }                              return $response;           │     │
│   │       return $next($request);      }                               │     │
│   │   }                                                              │     │
│   │                                                                  │     │
│   │   TERMINABLE MIDDLEWARE                                          │     │
│   │   ─────────────────────                                          │     │
│   │   public function terminate($request, $response)                 │     │
│   │   {                                                              │     │
│   │       // Executes AFTER response sent to browser                 │     │
│   │       // Good for logging, analytics                             │     │
│   │   }                                                              │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              MIDDLEWARE GROUPS                                   │     │
│   │                                                                  │     │
│   │   'web' => [                                                     │     │
│   │       EncryptCookies,                                            │     │
│   │       AddQueuedCookiesToResponse,                                │     │
│   │       StartSession,                                              │     │
│   │       ShareErrorsFromSession,                                    │     │
│   │       VerifyCsrfToken,                                           │     │
│   │       SubstituteBindings,                                        │     │
│   │   ],                                                             │     │
│   │                                                                  │     │
│   │   'api' => [                                                     │     │
│   │       ThrottleRequests,                                          │     │
│   │       SubstituteBindings,                                        │     │
│   │   ],                                                             │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Creating Middleware

**Definition:** You create new middleware using `php artisan make:middleware`. The class contains a `handle` method where you define logic to run before or after the request is processed by the application.

```bash
# Create middleware
php artisan make:middleware CheckRole
php artisan make:middleware EnsureTokenIsValid
```

```php
<?php
// app/Http/Middleware/CheckRole.php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class CheckRole
{
    /**
     * Handle an incoming request.
     *
     * @param  \Closure(\Illuminate\Http\Request): (\Symfony\Component\HttpFoundation\Response)  $next
     */
    public function handle(Request $request, Closure $next, string $role): Response
    {
        if (!$request->user() || !$request->user()->hasRole($role)) {
            // Redirect or abort
            return redirect('home');
            // OR
            abort(403, 'Unauthorized action.');
        }

        return $next($request);
    }
}
```

### Before/After Middleware

**Definition:** Middleware can perform tasks **before** the request reaches the application (e.g., checking authentication) or **after** the response is prepared (e.g., logging response time, adding headers). The timing depends on whether you perform actions before or after calling `$next($request)`.

```php
<?php
namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;

class BeforeMiddleware
{
    public function handle(Request $request, Closure $next): Response
    {
        // Actions BEFORE request is handled
        if (!$request->hasHeader('X-Api-Key')) {
            return response('API key missing', 401);
        }

        return $next($request);
    }
}

class AfterMiddleware
{
    public function handle(Request $request, Closure $next): Response
    {
        $response = $next($request);

        // Actions AFTER request is handled
        $response->header('X-Custom-Header', 'MyValue');

        return $response;
    }
}

class BeforeAndAfterMiddleware
{
    public function handle(Request $request, Closure $next): Response
    {
        // Before
        logger('Request started');

        $response = $next($request);

        // After
        logger('Request completed');

        return $response;
    }
}
```

### Registering Middleware

**Definition:** To activate middleware, it must be registered in the `app/Http/Kernel.php` file (or `bootstrap/app.php` in Laravel 11). You can register it globally (runs on every request), assign it to a group (like `web` or `api`), or alias it for use on individual routes.

**Global Middleware (app/Http/Kernel.php):**

```php
<?php
protected $middleware = [
    // \App\Http\Middleware\TrustHosts::class,
    \App\Http\Middleware\TrustProxies::class,
    \Illuminate\Http\Middleware\HandleCors::class,
    \App\Http\Middleware\PreventRequestsDuringMaintenance::class,
    \Illuminate\Foundation\Http\Middleware\ValidatePostSize::class,
    \App\Http\Middleware\TrimStrings::class,
    \Illuminate\Foundation\Http\Middleware\ConvertEmptyStringsToNull::class,
];
```

**Middleware Groups:**

```php
<?php
protected $middlewareGroups = [
    'web' => [
        \App\Http\Middleware\EncryptCookies::class,
        \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
        \Illuminate\Session\Middleware\StartSession::class,
        \Illuminate\View\Middleware\ShareErrorsFromSession::class,
        \App\Http\Middleware\VerifyCsrfToken::class,
        \Illuminate\Routing\Middleware\SubstituteBindings::class,
    ],

    'api' => [
        // \Laravel\Sanctum\Http\Middleware\EnsureFrontendRequestsAreStateful::class,
        'throttle:api',
        \Illuminate\Routing\Middleware\SubstituteBindings::class,
    ],
];
```

**Route Middleware (aliases):**

```php
<?php
protected $middlewareAliases = [
    'auth' => \App\Http\Middleware\Authenticate::class,
    'auth.basic' => \Illuminate\Auth\Middleware\AuthenticateWithBasicAuth::class,
    'auth.session' => \Illuminate\Session\Middleware\AuthenticateSession::class,
    'cache.headers' => \Illuminate\Http\Middleware\SetCacheHeaders::class,
    'can' => \Illuminate\Auth\Middleware\Authorize::class,
    'guest' => \App\Http\Middleware\RedirectIfAuthenticated::class,
    'password.confirm' => \Illuminate\Auth\Middleware\RequirePassword::class,
    'precognitive' => \Illuminate\Foundation\Http\Middleware\HandlePrecognitiveRequests::class,
    'signed' => \App\Http\Middleware\ValidateSignature::class,
    'throttle' => \Illuminate\Routing\Middleware\ThrottleRequests::class,
    'verified' => \Illuminate\Auth\Middleware\EnsureEmailIsVerified::class,
    'role' => \App\Http\Middleware\CheckRole::class,
];
```

**Applying Middleware:**

```php
<?php
// On route
Route::get('/admin', [AdminController::class, 'index'])
    ->middleware('auth');

// Multiple middleware
Route::get('/admin', [AdminController::class, 'index'])
    ->middleware(['auth', 'verified', 'role:admin']);

// With parameters
Route::get('/admin', [AdminController::class, 'index'])
    ->middleware('role:admin');

// On route group
Route::middleware(['auth', 'verified'])->group(function () {
    Route::get('/dashboard', [DashboardController::class, 'index']);
    Route::get('/settings', [SettingsController::class, 'index']);
});

// On controller
class AdminController extends Controller
{
    public function __construct()
    {
        $this->middleware('auth');
        $this->middleware('role:admin')->only('destroy');
        $this->middleware('log')->except('index');
    }
}

// Excluding middleware
Route::get('/public', [PublicController::class, 'index'])
    ->withoutMiddleware(['auth']);
```

### Terminable Middleware

**Definition:** Terminable middleware performs work *after* the HTTP response has implicitly been sent to the browser (e.g., complex logging or analytics). By implementing the `terminate` method, you ensure this heavy processing doesn't delay the page load for the user.

```php
<?php
namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class TerminableMiddleware
{
    public function handle(Request $request, Closure $next): Response
    {
        return $next($request);
    }

    public function terminate(Request $request, Response $response): void
    {
        // Execute after response sent to browser
        // Good for logging, analytics, etc.
        logger('Request completed', [
            'url' => $request->url(),
            'status' => $response->getStatusCode(),
        ]);
    }
}
```

---

## 11. Authentication

> **Definition:** Authentication is the process of verifying a user's identity. Laravel provides a complete authentication system with guards (how users are authenticated) and providers (where user data is retrieved from), supporting sessions, tokens, and third-party OAuth.

### Authentication Guards & Providers

**Definition:** **Guards** define *how* users are authenticated for each request (e.g., session-based for web, token-based for API). **Providers** define *how* users are retrieved from persistent storage (e.g., Eloquent query). This separation allows for flexible auth systems.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     AUTHENTICATION ARCHITECTURE                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              AUTHENTICATION COMPONENTS                           │     │
│   │                                                                  │     │
│   │   ┌──────────────┐    ┌──────────────┐    ┌──────────────┐      │     │
│   │   │    Guard     │    │   Provider   │    │   Session    │      │     │
│   │   ├──────────────┤    ├──────────────┤    ├──────────────┤      │     │
│   │   │ session      │    │ eloquent     │    │ Cookie       │      │     │
│   │   │ token        │    │ database     │    │ Store        │      │     │
│   │   │ sanctum      │    │ (custom)     │    │ Encrypted    │      │     │
│   │   └──────────────┘    └──────────────┘    └──────────────┘      │     │
│   │                                                                  │     │
│   │   ┌──────────────┐    ┌──────────────┐                          │     │
│   │   │  User Model  │    │  Password    │                          │     │
│   │   ├──────────────┤    ├──────────────┤                          │     │
│   │   │ Authenticable│    │ Bcrypt Hash  │                          │     │
│   │   │ RememberToken│    │ Verification │                          │     │
│   │   └──────────────┘    └──────────────┘                          │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              AUTHENTICATION FLOW                                 │     │
│   │                                                                  │     │
│   │   1. LOGIN ATTEMPT                                               │     │
│   │      ┌──────────┐                                                │     │
│   │      │  User    │──▶ POST /login (email, password)              │     │
│   │      └──────────┘                                                │     │
│   │            │                                                     │     │
│   │            ▼                                                     │     │
│   │   2. CREDENTIAL VALIDATION                                       │     │
│   │      ┌───────────────────┐                                       │     │
│   │      │ Auth::attempt()   │──▶ Provider finds user                │     │
│   │      │                   │──▶ Hash::check() password             │     │
│   │      └─────────┬─────────┘                                       │     │
│   │                │                                                 │     │
│   │      ┌─────────┴─────────┐                                       │     │
│   │      ▼                   ▼                                       │     │
│   │   Success            Failure                                     │     │
│   │      │                   │                                       │     │
│   │      ▼                   ▼                                       │     │
│   │   3. SESSION           Error                                     │     │
│   │      ┌───────────────────┐                                       │     │
│   │      │ Session Regen     │                                       │     │
│   │      │ Auth::login()     │                                       │     │
│   │      │ Redirect          │                                       │     │
│   │      └───────────────────┘                                       │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              MULTI-GUARD AUTHENTICATION                          │     │
│   │                                                                  │     │
│   │   ┌──────────┐         ┌──────────┐         ┌──────────┐        │     │
│   │   │   Web    │         │   API    │         │  Admin   │        │     │
│   │   │  Guard   │         │  Guard   │         │  Guard   │        │     │
│   │   └────┬─────┘         └────┬─────┘         └────┬─────┘        │     │
│   │        │                    │                    │               │     │
│   │        ▼                    ▼                    ▼               │     │
│   │   ┌──────────┐         ┌──────────┐         ┌──────────┐        │     │
│   │   │ Session  │         │  Token   │         │ Session  │        │     │
│   │   │ Cookie   │         │ Sanctum  │         │ Cookie   │        │     │
│   │   └──────────┘         └──────────┘         └──────────┘        │     │
│   │                                                                  │     │
│   │   Auth::guard('web')->check();                                   │     │
│   │   Auth::guard('api')->user();                                    │     │
│   │   Auth::guard('admin')->id();                                    │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Laravel Breeze

**Definition:** Laravel Breeze is a minimal, simple implementation of all of Laravel's authentication features, including login, registration, password reset, email verification, and password confirmation. It uses Blade templates and Tailwind CSS, making it a great starting point for new projects.

```bash
# Install Breeze
composer require laravel/breeze --dev

# Install with Livewire (default)
php artisan breeze:install livewire

# Or with Vue
php artisan breeze:install vue

# Or with React
php artisan breeze:install react

# Or with API only
php artisan breeze:install api

# Run migrations and build assets
php artisan migrate
npm install && npm run dev
```

### Laravel Jetstream

**Definition:** Laravel Jetstream is an application starter kit that provides a more advanced implementation of authentication. Beyond basic auth, it includes two-factor authentication, team management, browser session management, and API support via Sanctum, built with Livewire or Inertia.js.

```bash
# Install Jetstream
composer require laravel/jetstream

# With Livewire
php artisan jetstream:install livewire

# With Inertia
php artisan jetstream:install inertia

# With teams support
php artisan jetstream:install livewire --teams

# Run migrations and build
php artisan migrate
npm install && npm run dev
```

### Registration

**Definition:** Registration is the process of creating a new user record in the database. Laravel's starter kits handle validating input, hashing passwords (bcrypt), and firing the `Registered` event (which can trigger email verification).

```php
<?php
use App\Models\User;
use Illuminate\Support\Facades\Hash;

class RegisteredUserController extends Controller
{
    public function store(Request $request)
    {
        $request->validate([
            'name' => ['required', 'string', 'max:255'],
            'email' => ['required', 'string', 'email', 'max:255', 'unique:users'],
            'password' => ['required', 'confirmed', Rules\Password::defaults()],
        ]);

        $user = User::create([
            'name' => $request->name,
            'email' => $request->email,
            'password' => Hash::make($request->password),
        ]);

        event(new Registered($user));

        Auth::login($user);

        return redirect(RouteServiceProvider::HOME);
    }
}
```

### Login

**Definition:** Login authenticates a user by verifying their credentials (typically email and password). If successful, Laravel regenerates the session ID (to prevent fixation attacks) and stores the user's ID in the session, effectively logging them in.

```php
<?php
use Illuminate\Support\Facades\Auth;

class AuthenticatedSessionController extends Controller
{
    public function store(LoginRequest $request)
    {
        $request->authenticate();

        $request->session()->regenerate();

        return redirect()->intended(RouteServiceProvider::HOME);
    }

    public function destroy(Request $request)
    {
        Auth::guard('web')->logout();

        $request->session()->invalidate();
        $request->session()->regenerateToken();

        return redirect('/');
    }
}
```

### Password Reset

**Definition:** Laravel provides a secure, token-based password reset mechanism. It handles generating unique tokens, emailing reset links, verifying tokens, and updating passwords, protecting against common vulnerabilities like timing attacks.

```bash
php artisan make:notification ResetPasswordNotification
```

```php
<?php
// Send reset link
Password::sendResetLink(
    $request->only('email')
);

// Reset password
$status = Password::reset(
    $request->only('email', 'password', 'password_confirmation', 'token'),
    function (User $user, string $password) {
        $user->forceFill([
            'password' => Hash::make($password)
        ])->setRememberToken(Str::random(60));

        $user->save();

        event(new PasswordReset($user));
    }
);

return $status === Password::PASSWORD_RESET
    ? redirect()->route('login')->with('status', __($status))
    : back()->withErrors(['email' => [__($status)]]);
```

### Authentication Usage

**Definition:** Once authenticated, you can access the current user via the `Auth` facade (`Auth::user()`) or request helper (`$request->user()`). You can check if a user is logged in with `Auth::check()`, or get their ID with `Auth::id()`.

```php
<?php
use Illuminate\Support\Facades\Auth;

// Check if authenticated
if (Auth::check()) {
    // User is logged in
}

// Get current user
$user = Auth::user();
$name = Auth::user()->name;

// Get user ID
$id = Auth::id();

// Login
Auth::login($user);
Auth::login($user, $remember = true);

// Login once (no session)
Auth::once($credentials);

// Login using ID
Auth::loginUsingId(1);

// Attempt login
if (Auth::attempt(['email' => $email, 'password' => $password])) {
    // Authentication passed
}

// Attempt with remember
if (Auth::attempt($credentials, $remember)) {
    // ...
}

// Validate credentials only
if (Auth::validate($credentials)) {
    // Credentials are valid
}

// Logout
Auth::logout();

// Guard specific
Auth::guard('admin')->check();
Auth::guard('api')->user();

// In Blade
@auth
    <p>Welcome, {{ Auth::user()->name }}</p>
@endauth

@guest
    <a href="/login">Login</a>
@endguest
```

### Email Verification

**Definition:** Email verification ensures that the user provided a valid email address during registration. Laravel includes built-in support for sending verification links and middleware (`verified`) to restrict access to routes until the email is confirmed.

```php
<?php
// app/Models/User.php
use Illuminate\Contracts\Auth\MustVerifyEmail;

class User extends Authenticatable implements MustVerifyEmail
{
    // ...
}

// routes/web.php
Route::get('/email/verify', function () {
    return view('auth.verify-email');
})->middleware('auth')->name('verification.notice');

Route::get('/email/verify/{id}/{hash}', function (EmailVerificationRequest $request) {
    $request->fulfill();
    return redirect('/home');
})->middleware(['auth', 'signed'])->name('verification.verify');

Route::post('/email/verification-notification', function (Request $request) {
    $request->user()->sendEmailVerificationNotification();
    return back()->with('message', 'Verification link sent!');
})->middleware(['auth', 'throttle:6,1'])->name('verification.send');

// Protected routes
Route::get('/profile', function () {
    // Only verified users
})->middleware(['auth', 'verified']);
```

---

## 12. Authorization

> **Definition:** Authorization determines what actions an authenticated user is permitted to perform. Laravel provides two primary mechanisms: Gates (closure-based permissions) and Policies (class-based permissions organized around a specific model or resource).

### Authorization Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      AUTHORIZATION ARCHITECTURE                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              GATES VS POLICIES                                   │     │
│   │                                                                  │     │
│   │   GATES (Closure-Based)              POLICIES (Class-Based)      │     │
│   │   ─────────────────────              ─────────────────────       │     │
│   │                                                                  │     │
│   │   // Simple permission             // Model-specific rules       │     │
│   │   Gate::define('edit-post',        class PostPolicy              │     │
│   │   function ($user, $post) {        {                             │     │
│   │       return $user->id ===             public function update(   │     │
│   │              $post->user_id;               $user, $post)         │     │
│   │   });                                  {                         │     │
│   │                                        return $user->id ===      │     │
│   │   // No specific model                   $post->user_id;         │     │
│   │                                        }                         │     │
│   │                                    }                             │     │
│   │                                                                  │     │
│   │   Use for:                         Use for:                      │     │
│   │   - Simple checks                  - Resource CRUD               │     │
│   │   - Global permissions             - Model authorization         │     │
│   │   - One-off rules                  - Complex logic               │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              POLICY METHODS                                      │     │
│   │                                                                  │     │
│   │   viewAny()      ──▶ List all resources                        │     │
│   │   view()         ──▶ View specific resource                    │     │
│   │   create()       ──▶ Create new resource                       │     │
│   │   update()       ──▶ Edit existing resource                    │     │
│   │   delete()       ──▶ Soft delete resource                      │     │
│   │   restore()      ──▶ Restore soft-deleted resource             │     │
│   │   forceDelete()  ──▶ Permanently delete resource               │     │
│   │                                                                  │     │
│   │   before()       ──▶ Run before all methods (e.g., superadmin) │     │
│   │                                                                  │     │
│   │   RESOURCE CONTROLLER MAPPING:                                   │     │
│   │   index()   ──▶ viewAny()    destroy()  ──▶ delete()             │     │
│   │   create()  ──▶ create()     restore()  ──▶ restore()            │     │
│   │   store()   ──▶ create()     forceDelete() ──▶ forceDelete()     │     │
│   │   show()    ──▶ view()                                           │     │
│   │   edit()    ──▶ update()                                         │     │
│   │   update()  ──▶ update()                                         │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              AUTHORIZATION CHECKS                                │     │
│   │                                                                  │     │
│   │   In Controllers:                                                │     │
│   │   ───────────────                                                │     │
│   │   $this->authorize('update', $post);                             │     │
│   │   $this->authorize(Post::class);  // Auto-resolves               │     │
│   │                                                                  │     │
│   │   Via Gate Facade:                                               │     │
│   │   ────────────────                                               │     │
│   │   Gate::allows('edit-post', $post)                               │     │
│   │   Gate::denies('delete-post', $post)                             │     │
│   │   Gate::authorize('update', $post)  // Throws if denied          │     │
│   │                                                                  │     │
│   │   Via User Model:                                                │     │
│   │   ───────────────                                                │     │
│   │   $user->can('update', $post)                                    │     │
│   │   $user->cannot('delete', $post)                                 │     │
│   │   $user->canAny(['update', 'delete'], $post)                     │     │
│   │                                                                  │     │
│   │   In Routes:                                                     │     │
│   │   ─────────                                                      │     │
│   │   Route::put('/posts/{post}', [PostController::class, 'update']) │     │
│   │       ->middleware('can:update,post');                           │     │
│   │                                                                  │     │
│   │   In Blade:                                                      │     │
│   │   ─────────                                                      │     │
│   │   @can('update', $post)                                          │     │
│   │       <a href="{{ route('posts.edit', $post) }}">Edit</a>         │     │
│   │   @endcan                                                        │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Gates

**Definition:** Gates are closures that determine if a user is authorized to perform a given action. They are typically defined in the `AppServiceProvider`. Gates are best for simple, resource-indepedent checks (e.g., `Gate::allows('access-admin-panel')`).

```php
<?php
// app/Providers/AuthServiceProvider.php

use App\Models\Post;
use App\Models\User;
use Illuminate\Support\Facades\Gate;

class AuthServiceProvider extends ServiceProvider
{
    public function boot(): void
    {
        // Define gates
        Gate::define('edit-post', function (User $user, Post $post) {
            return $user->id === $post->user_id;
        });

        Gate::define('delete-post', function (User $user, Post $post) {
            return $user->id === $post->user_id || $user->isAdmin();
        });

        // Using closure
        Gate::define('create-post', function (User $user) {
            return $user->role === 'author' || $user->role === 'admin';
        });

        // Guest users (before authentication)
        Gate::define('view-post', function (?User $user, Post $post) {
            return $post->isPublished() || ($user && $user->id === $post->user_id);
        });
    }
}
```

### Policies

```bash
# Create policy
php artisan make:policy PostPolicy

# Create with model
php artisan make:policy PostPolicy --model=Post
```

```php
<?php
// app/Policies/PostPolicy.php

namespace App\Policies;

use App\Models\Post;
use App\Models\User;

class PostPolicy
{
    /**
     * Determine whether the user can view any models.
     */
    public function viewAny(User $user): bool
    {
        return true;
    }

    /**
     * Determine whether the user can view the model.
     */
    public function view(User $user, Post $post): bool
    {
        return $post->isPublished() || $user->id === $post->user_id;
    }

    /**
     * Determine whether the user can create models.
     */
    public function create(User $user): bool
    {
        return $user->isAuthor() || $user->isAdmin();
    }

    /**
     * Determine whether the user can update the model.
     */
    public function update(User $user, Post $post): bool
    {
        return $user->id === $post->user_id;
    }

    /**
     * Determine whether the user can delete the model.
     */
    public function delete(User $user, Post $post): bool
    {
        return $user->id === $post->user_id || $user->isAdmin();
    }

    /**
     * Determine whether the user can restore the model.
     */
    public function restore(User $user, Post $post): bool
    {
        return $user->isAdmin();
    }

    /**
     * Determine whether the user can permanently delete the model.
     */
    public function forceDelete(User $user, Post $post): bool
    {
        return $user->isAdmin();
    }

    /**
     * Admin can do anything.
     */
    public function before(User $user, string $ability): ?bool
    {
        if ($user->isSuperAdmin()) {
            return true;
        }

        return null;
    }
}
```

**Register Policy:**

```php
<?php
// app/Providers/AuthServiceProvider.php

protected $policies = [
    Post::class => PostPolicy::class,
    Comment::class => CommentPolicy::class,
];
```

### Authorizing Actions

```php
<?php
use Illuminate\Support\Facades\Gate;
use Illuminate\Support\Facades\Auth;

// Via Gate facade
if (Gate::allows('edit-post', $post)) {
    // User can edit post
}

if (Gate::denies('edit-post', $post)) {
    abort(403);
}

// For specific user
if (Gate::forUser($user)->allows('edit-post', $post)) {
    // ...
}

// Via authorize helper
$this->authorize('update', $post);

// Authorize and throw exception
Gate::authorize('edit-post', $post);

// Check any/none
if (Gate::any(['update', 'delete'], $post)) {
    // User can update OR delete
}

if (Gate::none(['update', 'delete'], $post)) {
    // User can neither update NOR delete
}

// Via User model
if ($request->user()->can('update', $post)) {
    // ...
}

if ($request->user()->cannot('update', $post)) {
    // ...
}
```

**In Controllers:**

```php
<?php
class PostController extends Controller
{
    public function update(Request $request, Post $post)
    {
        $this->authorize('update', $post);

        // Update post...
    }

    public function edit(Post $post)
    {
        // Authorize via middleware
        return view('posts.edit', compact('post'));
    }
}

// Route middleware
Route::put('/posts/{post}', [PostController::class, 'update'])
    ->middleware('can:update,post');

// Resource with policy
Route::resource('posts', PostController::class)
    ->middleware('auth');
```

### Blade Directives

```blade
{{-- @can --}}
@can('update', $post)
    <a href="{{ route('posts.edit', $post) }}">Edit</a>
@endcan

{{-- @cannot --}}
@cannot('update', $post)
    <p>You cannot edit this post.</p>
@endcannot

{{-- @elsecan --}}
@can('update', $post)
    <a href="{{ route('posts.edit', $post) }}">Edit</a>
@elsecan('create', App\Models\Post::class)
    <a href="{{ route('posts.create') }}">Create New Post</a>
@endcan

{{-- Multiple actions --}}
@canany(['update', 'delete'], $post)
    <form action="{{ route('posts.destroy', $post) }}" method="POST">
        @csrf
        @method('DELETE')
        <button>Delete</button>
    </form>
@endcanany

{{-- @guest --}}
@guest
    <a href="/login">Login to edit</a>
@endguest

{{-- Policy model binding --}}
@can('view', $post)
    {{ $post->content }}
@endcan
```

---

## 13. File Storage

> **Definition:** Laravel's File Storage provides a unified API for file operations across multiple storage systems (local disk, S3, FTP, etc.). The Storage facade offers a consistent interface for uploading, retrieving, and managing files regardless of the underlying storage provider.

### Storage Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      FILE STORAGE ARCHITECTURE                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              STORAGE DISKS                                       │     │
│   │                                                                  │     │
│   │   ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐        │     │
│   │   │  Local   │  │  Public  │  │   S3     │  │  Custom  │        │     │
│   │   │  Disk    │  │  Disk    │  │  Driver  │  │  Driver  │        │     │
│   │   ├──────────┤  ├──────────┤  ├──────────┤  ├──────────┤        │     │
│   │   │ Private  │  │ Public   │  │ Cloud    │  │ FTP      │        │     │
│   │   │ storage/ │  │ storage/ │  │ Storage  │  │ SFTP     │        │     │
│   │   │ app/     │  │ public/  │  │ AWS S3   │  │ etc.     │        │     │
│   │   └──────────┘  └──────────┘  └──────────┘  └──────────┘        │     │
│   │                                                                  │     │
│   │   Storage::disk('local')->put('file.txt', $content)              │     │
│   │   Storage::disk('public')->url('file.txt')                       │     │
│   │   Storage::disk('s3')->put('path/file.txt', $content)            │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              FILE UPLOAD FLOW                                    │     │
│   │                                                                  │     │
│   │   1. Request Validation                                          │     │
│   │      $request->validate(['avatar' => 'required|image|max:2048']) │     │
│   │                              │                                   │     │
│   │                              ▼                                   │     │
│   │   2. Get Uploaded File                                           │     │
│   │      $file = $request->file('avatar')                            │     │
│   │                              │                                   │     │
│   │                              ▼                                   │     │
│   │   3. Store File                                                  │     │
│   │      ┌─────────────────────────────────────────────────────┐    │     │
│   │      │ store('path')           ──▶ Auto hash filename      │    │     │
│   │      │ storeAs('path', 'name') ──▶ Custom filename          │    │     │
│   │      │ storePublicly('path')   ──▶ Public visibility        │    │     │
│   │      └─────────────────────────────────────────────────────┘    │     │
│   │                              │                                   │     │
│   │                              ▼                                   │     │
│   │   4. Get Path/URL                                                │     │
│   │      $path = 'avatars/abc123.jpg'                                │     │
│   │      $url = Storage::url($path)  ──▶ /storage/avatars/...        │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              STORAGE OPERATIONS                                  │     │
│   │                                                                  │     │
│   │   Write Operations        Read Operations      File Info         │     │
│   │   ─────────────────       ───────────────      ─────────         │     │
│   │                                                                  │     │
│   │   put()                   get()                exists()          │     │
│   │   append()                download()           missing()         │     │
│   │   prepend()               url()                size()            │     │
│   │   copy()                  temporaryUrl()       lastModified()    │     │
│   │   move()                                                       │     │
│   │   delete()                                                     │     │
│   │                                                                  │     │
│   │   Directories                                                    │     │
│   │   ───────────                                                    │     │
│   │   makeDirectory()                                                │     │
│   │   deleteDirectory()                                              │     │
│   │   files()                                                        │     │
│   │   allFiles()                                                     │     │
│   │   directories()                                                  │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              PUBLIC DISK SETUP                                   │     │
│   │                                                                  │     │
│   │   1. Configure filesystems.php                                   │     │
│   │      'public' => [                                               │     │
│   │          'driver' => 'local',                                    │     │
│   │          'root' => storage_path('app/public'),                   │     │
│   │          'url' => env('APP_URL').'/storage',                     │     │
│   │          'visibility' => 'public',                               │     │
│   │      ],                                                          │     │
│   │                                                                  │     │
│   │   2. Create symbolic link                                        │     │
│   │      php artisan storage:link                                    │     │
│   │      // Creates: public/storage ──▶ storage/app/public           │     │
│   │                                                                  │     │
│   │   3. Access in Blade                                             │     │
│   │      <img src="{{ asset('storage/avatars/user.jpg') }}">         │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Uploading Files

**Definition:** Laravel handles file uploads via the `Illuminate\Http\UploadedFile` instance available on the request. You can store uploaded files using the `store()` method, which automatically generates a unique ID for the filename and saves it to your configured disk.

```php
<?php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Storage;

class FileController extends Controller
{
    public function upload(Request $request)
    {
        $request->validate([
            'avatar' => 'required|image|mimes:jpg,png,jpeg,gif|max:2048',
        ]);

        // Store uploaded file
        if ($request->hasFile('avatar')) {
            $file = $request->file('avatar');
            
            // Store with original name
            $path = $file->store('avatars');
            
            // Store with custom name
            $path = $file->storeAs('avatars', 'custom-name.jpg');
            
            // Store on specific disk
            $path = $file->store('avatars', 's3');
            
            // Store with visibility
            $path = $file->storePublicly('avatars');
            $path = $file->storePubliclyAs('avatars', 'public-avatar.jpg');
            
            // Get file info
            $originalName = $file->getClientOriginalName();
            $extension = $file->getClientOriginalExtension();
            $mimeType = $file->getMimeType();
            $size = $file->getSize();
            
            // Check if valid
            if ($file->isValid()) {
                // Store it
            }
            
            // Store with hash name (recommended)
            $path = $file->store('avatars', ['disk' => 'public']);
            
            return response()->json([
                'path' => $path,
                'url' => Storage::url($path),
            ]);
        }
    }
}
```

### Storage Facade

**Definition:** The `Storage` facade provides a powerful abstraction for interacting with your configured file disks. It allows you to switch between local storage and cloud providers (like Amazon S3) by simply changing a configuration value, without modifying your code.

```php
<?php
use Illuminate\Support\Facades\Storage;

// Store content
Storage::put('file.txt', 'Contents');
Storage::put('file.txt', $resource); // From stream

// Append to file
Storage::append('file.txt', 'More content');

// Prepend to file
Storage::prepend('file.txt', 'First line');

// Get content
$contents = Storage::get('file.txt');

// Check existence
if (Storage::exists('file.txt')) {
    // ...
}

if (Storage::missing('file.txt')) {
    // ...
}

// Download file
return Storage::download('file.txt');
return Storage::download('file.txt', 'custom-name.txt');

// Get file info
$size = Storage::size('file.txt');
$time = Storage::lastModified('file.txt');

// Copy/Move
Storage::copy('old/file.txt', 'new/file.txt');
Storage::move('old/file.txt', 'new/file.txt');

// Rename
Storage::rename('old.txt', 'new.txt');

// Delete
Storage::delete('file.txt');
Storage::delete(['file1.txt', 'file2.txt']);

// Directories
Storage::makeDirectory('directory');
Storage::deleteDirectory('directory');

// Files in directory
$files = Storage::files('directory');
$allFiles = Storage::allFiles('directory');

// Directories
$directories = Storage::directories('directory');
$allDirectories = Storage::allDirectories('directory');

// Specific disk
Storage::disk('s3')->put('avatars/1/file.png', $content);
Storage::disk('public')->url('file.txt');

// Temporary URL (for private files)
$url = Storage::temporaryUrl(
    'file.jpg',
    now()->addMinutes(5)
);

// Upload pre-signed URL
$url = Storage::temporaryUploadUrl(
    'file.jpg',
    now()->addMinutes(5)
);
```

### Disks Configuration

```php
<?php
// config/filesystems.php

return [
    'default' => env('FILESYSTEM_DISK', 'local'),

    'disks' => [
        'local' => [
            'driver' => 'local',
            'root' => storage_path('app'),
            'throw' => false,
        ],

        'public' => [
            'driver' => 'local',
            'root' => storage_path('app/public'),
            'url' => env('APP_URL').'/storage',
            'visibility' => 'public',
            'throw' => false,
        ],

        's3' => [
            'driver' => 's3',
            'key' => env('AWS_ACCESS_KEY_ID'),
            'secret' => env('AWS_SECRET_ACCESS_KEY'),
            'region' => env('AWS_DEFAULT_REGION'),
            'bucket' => env('AWS_BUCKET'),
            'url' => env('AWS_URL'),
            'endpoint' => env('AWS_ENDPOINT'),
            'use_path_style_endpoint' => env('AWS_USE_PATH_STYLE_ENDPOINT', false),
            'throw' => false,
        ],

        'ftp' => [
            'driver' => 'ftp',
            'host' => env('FTP_HOST'),
            'username' => env('FTP_USERNAME'),
            'password' => env('FTP_PASSWORD'),
            'root' => '',
        ],
    ],

    'links' => [
        public_path('storage') => storage_path('app/public'),
    ],
];
```

### Public Disk & URLs

**Definition:** The `public` disk is intended for files that should be publicly accessible (like user avatars). To serve these files, you must create a symbolic link from `public/storage` to `storage/app/public` using `php artisan storage:link`, making them accessible via URL.

```bash
# Create symbolic link (required for public disk)
php artisan storage:link
```

```php
<?php
// Store file in public disk
$path = $request->file('avatar')->store('avatars', 'public');

// Generate URL
$url = Storage::disk('public')->url($path);
// /storage/avatars/xyz.jpg

// In Blade
<img src="{{ asset('storage/' . $path) }}" alt="Avatar">

// Or use Storage facade
<img src="{{ Storage::url($path) }}" alt="Avatar">

// Check if file exists
@if(Storage::disk('public')->exists($path))
    <img src="{{ Storage::url($path) }}">
@endif
```

---

## 14. API Development

> **Definition:** API Development in Laravel involves creating stateless HTTP endpoints that return JSON responses. Laravel provides specialized tools including API routes, resource controllers, API Resources for data transformation, and Sanctum for token-based authentication.

### API Resource Transformation

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      API RESOURCE ARCHITECTURE                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              API RESOURCE FLOW                                   │     │
│   │                                                                  │     │
│   │   Eloquent Model ──▶ API Resource ──▶ JSON Response              │     │
│   │                                                                  │     │
│   │   ┌──────────┐      ┌──────────┐      ┌──────────┐              │     │
│   │   │   User   │─────▶│UserResource│─────▶│  JSON    │              │     │
│   │   │  Model   │      │Transform │      │ Response │              │     │
│   │   │          │      │          │      │          │              │     │
│   │   │id: 1     │      │id: 1     │      │{"id":1   │              │     │
│   │   │name:"John│      │name:"John│      │"name":"Jo│              │     │
│   │   │email:...│      │email:... │      │"email":..│              │     │
│   │   │password  │      │(hidden)  │      │}          │              │     │
│   │   │is_admin  │      │(cond.)   │      │           │              │     │
│   │   └──────────┘      └──────────┘      └──────────┘              │     │
│   │                                                                  │     │
│   │   Transforms raw model data into API-friendly format             │     │
│   │   • Hides sensitive fields                                       │     │
│   │   • Formats dates and values                                     │     │
│   │   • Includes conditional fields                                  │     │
│   │   • Handles relationships                                        │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              RESOURCE METHODS                                    │     │
│   │                                                                  │     │
│   │   toArray()                    ──▶ Define transformed fields    │     │
│   │                                                                  │     │
│   │   Conditional Methods:                                           │     │
│   │   ─────────────────────                                          │     │
│   │   $this->when($condition, $value)  ──▶ Include if condition     │     │
│   │   $this->mergeWhen($condition, $array)                           │     │
│   │   $this->whenLoaded('relationship') ──▶ Include if eager loaded │     │
│   │   $this->whenCounted('relationship') ──▶ Include count          │     │
│   │   $this->whenPivotLoaded('table', $callback)                     │     │
│   │                                                                  │     │
│   │   Response Methods:                                              │     │
│   │   ─────────────────                                              │     │
│   │   ->response()                   ──▶ Customize response         │     │
│   │   ->additional(['meta' => ...])  ──▶ Add metadata               │     │
│   │   ->with(['key' => 'value'])     ──▶ Add wrapper                │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              API RESPONSE STRUCTURE                              │     │
│   │                                                                  │     │
│   │   Single Resource:                                               │     │
│   │   ────────────────                                               │     │
│   │   {                                                              │     │
│   │       "id": 1,                                                   │     │
│   │       "name": "John Doe",                                        │     │
│   │       "email": "john@example.com",                               │     │
│   │       "created_at": "2024-01-15"                                 │     │
│   │   }                                                              │     │
│   │                                                                  │     │
│   │   Resource Collection:                                           │     │
│   │   ───────────────────                                            │     │
│   │   {                                                              │     │
│   │       "data": [...],                                             │     │
│   │       "meta": {                                                  │     │
│   │           "current_page": 1,                                     │     │
│   │           "last_page": 10,                                       │     │
│   │           "per_page": 15,                                        │     │
│   │           "total": 150                                           │     │
│   │       },                                                         │     │
│   │       "links": {                                                 │     │
│   │           "first": "...",                                        │     │
│   │           "last": "...",                                         │     │
│   │           "prev": null,                                          │     │
│   │           "next": "..."                                          │     │
│   │       }                                                          │     │
│   │   }                                                              │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              HTTP STATUS CODES                                   │     │
│   │                                                                  │     │
│   │   Success (2xx)              Client Errors (4xx)                 │     │
│   │   ───────────────            ───────────────────                 │     │
│   │   200 OK                     400 Bad Request                     │     │
│   │   201 Created                401 Unauthorized                    │     │
│   │   204 No Content             403 Forbidden                       │     │
│   │                              404 Not Found                       │     │
│   │   Server Errors (5xx)        422 Unprocessable Entity            │     │
│   │   ─────────────────          429 Too Many Requests               │     │
│   │   500 Internal Server Error                                      │     │
│   │                                                                  │     │
│   │   Response::HTTP_OK                                              │     │
│   │   Response::HTTP_CREATED                                         │     │
│   │   Response::HTTP_UNPROCESSABLE_ENTITY                            │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
│   ┌──────────────────────────────────────────────────────────────────┐     │
│   │              SANCTUM TOKEN FLOW                                  │     │
│   │                                                                  │     │
│   │   1. Login                                                       │     │
│   │      POST /api/login (email, password)                          │     │
│   │              │                                                   │     │
│   │              ▼                                                   │     │
│   │      Validate Credentials                                        │     │
│   │              │                                                   │     │
│   │              ▼                                                   │     │
│   │      $user->createToken('device-name')                           │     │
│   │              │                                                   │     │
│   │              ▼                                                   │     │
│   │      Return: {                                                   │     │
│   │          user: {...},                                            │     │
│   │          token: "1|abc123..."  ──▶ Plain text token             │     │
│   │      }                                                           │     │
│   │                                                                  │     │
│   │   2. Authenticated Request                                       │     │
│   │      Header: Authorization: Bearer 1|abc123...                   │     │
│   │              │                                                   │     │
│   │              ▼                                                   │     │
│   │      middleware('auth:sanctum')                                  │     │
│   │              │                                                   │     │
│   │              ▼                                                   │     │
│   │      Resolve User from Token                                     │     │
│   │              │                                                   │     │
│   │              ▼                                                   │     │
│   │      Process Request                                             │     │
│   │                                                                  │     │
│   │   3. Logout                                                      │     │
│   │      $request->user()->currentAccessToken()->delete()            │     │
│   │                                                                  │     │
│   └──────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### API Routes

**Definition:** API routes are defined in `routes/api.php` and are assigned the `api` middleware group. Unlike web routes, they are stateless (no session/cookies) and typically use token-based authentication. They are prefixed with `/api` by default.

```php
<?php
// routes/api.php

use Illuminate\Support\Facades\Route;

Route::get('/users', [UserController::class, 'index']);
Route::get('/users/{user}', [UserController::class, 'show']);
Route::post('/users', [UserController::class, 'store']);
Route::put('/users/{user}', [UserController::class, 'update']);
Route::delete('/users/{user}', [UserController::class, 'destroy']);

// API Resource (no create/edit routes)
Route::apiResource('posts', PostController::class);

// Nested API resources
Route::apiResource('posts.comments', CommentController::class)->shallow();

// Route group with middleware
Route::middleware('auth:sanctum')->group(function () {
    Route::get('/user', function (Request $request) {
        return $request->user();
    });
    
    Route::apiResource('posts', PostController::class);
});

// Versioning
Route::prefix('v1')->group(function () {
    Route::apiResource('users', Api\V1\UserController::class);
});

Route::prefix('v2')->group(function () {
    Route::apiResource('users', Api\V2\UserController::class);
});
```

### API Resources

**Definition:** API Resources (and Resource Collections) act as a transformation layer between your Eloquent models and the JSON response returned to the API client. They allow you to granularly control which data is exposed and format it (e.g., renaming fields, adding links) consistently.

```bash
# Create resource
php artisan make:resource UserResource

# Create resource collection
php artisan make:resource UserCollection
```

**Basic Resource:**

```php
<?php
// app/Http/Resources/UserResource.php

namespace App\Http\Resources;

use Illuminate\Http\Request;
use Illuminate\Http\Resources\Json\JsonResource;

class UserResource extends JsonResource
{
    public function toArray(Request $request): array
    {
        return [
            'id' => $this->id,
            'name' => $this->name,
            'email' => $this->email,
            'avatar' => $this->avatar_url,
            'member_since' => $this->created_at->format('M d, Y'),
            'posts_count' => $this->whenCounted('posts'),
            
            // Conditional fields
            'email_verified' => $this->when(
                $request->user()?->isAdmin(),
                $this->email_verified_at
            ),
            
            // Merge when
            $this->mergeWhen($request->user()?->id === $this->id, [
                'last_login' => $this->last_login_at,
                'settings' => $this->settings,
            ]),
            
            // Relationships
            'posts' => PostResource::collection($this->whenLoaded('posts')),
            'profile' => new ProfileResource($this->whenLoaded('profile')),
            
            // Links
            'links' => [
                'self' => route('api.users.show', $this->id),
                'posts' => route('api.users.posts.index', $this->id),
            ],
        ];
    }
}
```

**Resource Collection:**

```php
<?php
// app/Http/Resources/UserCollection.php

namespace App\Http\Resources;

use Illuminate\Http\Request;
use Illuminate\Http\Resources\Json\ResourceCollection;

class UserCollection extends ResourceCollection
{
    public function toArray(Request $request): array
    {
        return [
            'data' => $this->collection,
            'meta' => [
                'total' => $this->total(),
                'count' => $this->count(),
                'per_page' => $this->perPage(),
                'current_page' => $this->currentPage(),
                'total_pages' => $this->lastPage(),
            ],
            'links' => [
                'self' => $this->url($this->currentPage()),
                'first' => $this->url(1),
                'last' => $this->url($this->lastPage()),
                'prev' => $this->previousPageUrl(),
                'next' => $this->nextPageUrl(),
            ],
        ];
    }
}
```

**Using Resources:**

```php
<?php
namespace App\Http\Controllers\Api;

use App\Http\Resources\UserResource;
use App\Http\Resources\UserCollection;
use App\Models\User;

class UserController extends Controller
{
    public function index()
    {
        $users = User::paginate(10);
        
        return new UserCollection($users);
    }

    public function show(User $user)
    {
        return new UserResource($user);
    }

    public function store(Request $request)
    {
        $user = User::create($request->validated());
        
        return (new UserResource($user))
            ->response()
            ->setStatusCode(201);
    }

    public function me(Request $request)
    {
        return new UserResource($request->user());
    }
}
```

### API Responses

```php
<?nphp
// Successful response
return response()->json([
    'data' => $users,
    'message' => 'Users retrieved successfully',
]);

// With status code
return response()->json([
    'message' => 'Created successfully',
], 201);

// Error response
return response()->json([
    'message' => 'Validation failed',
    'errors' => [
        'email' => ['The email field is required.'],
    ],
], 422);

// No content
return response()->noContent();

// Not found
return response()->json([
    'message' => 'Resource not found',
], 404);

// Custom headers
return response()
    ->json(['data' => $users])
    ->header('X-Total-Count', 100);

// With resource
return UserResource::collection($users);

// Additional data
return (new UserResource($user))
    ->additional(['meta' => ['version' => '1.0']]);

// Wrap resource
return UserResource::collection($users)->wrap('users');
```

### Sanctum Authentication

**Definition:** Laravel Sanctum is a lightweight authentication system for SPAs (Single Page Applications) and simple APIs. It allows users to generate multiple API tokens for their account, and provides a simple way to authenticate SPA requests using cookies via CSRF protection.

```bash
# Install Sanctum
composer require laravel/sanctum

# Publish config
php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"

# Run migrations
php artisan migrate

# Add trait to User model
```

```php
<?php
// app/Models/User.php

use Laravel\Sanctum\HasApiTokens;

class User extends Authenticatable
{
    use HasApiTokens, HasFactory, Notifiable;
}
```

```php
<?php
// routes/api.php

use Illuminate\Support\Facades\Route;

// Public routes
Route::post('/register', [AuthController::class, 'register']);
Route::post('/login', [AuthController::class, 'login']);

// Protected routes
Route::middleware('auth:sanctum')->group(function () {
    Route::get('/user', function (Request $request) {
        return $request->user();
    });
    
    Route::post('/logout', [AuthController::class, 'logout']);
    Route::apiResource('posts', PostController::class);
});
```

**Auth Controller:**

```php
<?php
namespace App\Http\Controllers\Api;

use App\Models\User;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Hash;
use Illuminate\Validation\ValidationException;

class AuthController extends Controller
{
    public function register(Request $request)
    {
        $request->validate([
            'name' => 'required|string|max:255',
            'email' => 'required|string|email|max:255|unique:users',
            'password' => 'required|string|min:8|confirmed',
        ]);

        $user = User::create([
            'name' => $request->name,
            'email' => $request->email,
            'password' => Hash::make($request->password),
        ]);

        $token = $user->createToken('auth_token')->plainTextToken;

        return response()->json([
            'user' => $user,
            'token' => $token,
        ], 201);
    }

    public function login(Request $request)
    {
        $request->validate([
            'email' => 'required|email',
            'password' => 'required',
            'device_name' => 'required',
        ]);

        $user = User::where('email', $request->email)->first();

        if (!$user || !Hash::check($request->password, $user->password)) {
            throw ValidationException::withMessages([
                'email' => ['The provided credentials are incorrect.'],
            ]);
        }

        $token = $user->createToken($request->device_name)->plainTextToken;

        return response()->json([
            'user' => $user,
            'token' => $token,
        ]);
    }

    public function logout(Request $request)
    {
        // Revoke current token
        $request->user()->currentAccessToken()->delete();
        
        // OR revoke all tokens
        // $request->user()->tokens()->delete();

        return response()->json([
            'message' => 'Logged out successfully',
        ]);
    }
}
```

**Token Abilities:**

```php
<?php
// Create token with abilities
$token = $user->createToken('token-name', ['posts:read', 'posts:create'])->plainTextToken;

// Check abilities
if ($request->user()->tokenCan('posts:delete')) {
    // User can delete posts
}

// Middleware for abilities
Route::post('/posts', [PostController::class, 'store'])
    ->middleware('auth:sanctum', 'abilities:posts:create');

Route::delete('/posts/{post}', [PostController::class, 'destroy'])
    ->middleware('auth:sanctum', 'abilities:posts:delete');

// OR check any ability
Route::middleware('auth:sanctum', 'ability:posts:create,posts:update')->group(function () {
    // ...
});
```

### API Best Practices

```php
<?php
// 1. Use API Resources for consistent responses
return new UserResource($user);

// 2. Return proper HTTP status codes
// 200 OK - Successful GET, PUT, DELETE
// 201 Created - Successful POST
// 204 No Content - Successful DELETE with no body
// 400 Bad Request - Validation error
// 401 Unauthorized - Not authenticated
// 403 Forbidden - Not authorized
// 404 Not Found - Resource not found
// 422 Unprocessable Entity - Validation error
// 500 Internal Server Error - Server error

// 3. Use Form Requests for validation
public function store(StoreUserRequest $request)
{
    $user = User::create($request->validated());
    return new UserResource($user);
}

// 4. Handle errors consistently
// app/Exceptions/Handler.php
public function register(): void
{
    $this->renderable(function (NotFoundHttpException $e, $request) {
        if ($request->is('api/*')) {
            return response()->json([
                'message' => 'Resource not found.',
            ], 404);
        }
    });
}

// 5. Version your API
Route::prefix('v1')->group(function () {
    Route::apiResource('users', Api\V1\UserController::class);
});

// 6. Use resourceful naming
// GET    /api/users       -> index
// GET    /api/users/1     -> show
// POST   /api/users       -> store
// PUT    /api/users/1     -> update
// DELETE /api/users/1     -> destroy

// 7. Include pagination metadata
$users = User::paginate(10);
return UserResource::collection($users);

// 8. Use eager loading to avoid N+1
$users = User::with('posts')->get();

// 9. Rate limiting (in RouteServiceProvider)
RateLimiter::for('api', function (Request $request) {
    return Limit::perMinute(60)->by($request->user()?->id ?: $request->ip());
});
```

---

## Best Practices Summary

### General
- Follow PSR-12 coding standards
- Use meaningful variable and method names
- Keep controllers thin, models rich
- Use dependency injection
- Write tests for your code

### Database
- Always use migrations for schema changes
- Use factories for test data
- Index frequently queried columns
- Use transactions for multiple operations
- Never commit `.env` files

### Security
- Validate all input
- Use prepared statements (Eloquent does this automatically)
- Hash passwords with bcrypt
- Use CSRF protection for web routes
- Implement proper authorization checks
- Store sensitive files outside web root

### Performance
- Use eager loading to prevent N+1 queries
- Cache frequently accessed data
- Use database transactions for batch operations
- Implement pagination for large datasets
- Use queues for long-running tasks

### API Development
- Version your APIs from the start
- Use proper HTTP status codes
- Implement rate limiting
- Document your API
- Return consistent response formats
- Use API Resources

---

*This documentation covers the core concepts of Laravel. For more advanced topics like Queues, Events, Broadcasting, and Testing, refer to the official Laravel documentation at https://laravel.com/docs.*

---

## 15. Caching

**Definition:** Caching stores the results of expensive operations (database queries, API calls, computed values) so subsequent requests can be served faster. Laravel provides a unified caching API that supports multiple backends (file, Redis, Memcached, database, array).

### Cache Drivers

**Definition:** Laravel supports various cache backends (drivers) via a unified API. Common drivers include `file` (default, good for local dev), `database`, `redis`, and `memcached`. Using a fast, in-memory cache like Redis significantly improves application performance by reducing database load.

| Driver | Use Case | Config |
|--------|----------|--------|
| `file` | Simple apps, development | Default |
| `redis` | Production, high performance | Requires Redis |
| `memcached` | Production, distributed | Requires Memcached |
| `database` | No extra infrastructure | Slower than Redis |
| `array` | Testing (in-memory, per-request) | Tests only |

Configure in `.env`:
```env
CACHE_DRIVER=redis
REDIS_HOST=127.0.0.1
REDIS_PORT=6379
```

### Basic Cache Operations

**Definition:** The `Cache` facade allows you to store (`put`), retrieve (`get`), and verify (`has`) cached items. If a key doesn't exist, `get` can return a default value or execute a closure. Storing computed data effectively avoids expensive recalculations.

```php
use Illuminate\Support\Facades\Cache;

// Store a value for 60 seconds
Cache::put('key', 'value', 60);

// Store forever
Cache::forever('key', 'value');

// Retrieve (with default)
$value = Cache::get('key', 'default');

// Check existence
if (Cache::has('key')) { ... }

// Remove
Cache::forget('key');

// Flush all cache
Cache::flush();

// Retrieve and delete
$value = Cache::pull('key');
```

### Cache Remember (Most Common Pattern)

**Definition:** The `Cache::remember` method is the most efficient way to handle caching. It attempts to retrieve an item from the cache; if successful, it returns it. If missing, it executes the provided closure, stores the result in the cache for the specified time, and *then* returns it.

```php
// Fetch from cache, or execute closure and cache result
$users = Cache::remember('users', 3600, function () {
    return User::with('roles')->get();
});

// Remember forever
$settings = Cache::rememberForever('settings', function () {
    return Setting::all()->keyBy('key');
});
```

### Cache Tags (Redis / Memcached only)

**Definition:** Cache tags allow you to tag related items in the cache and then flush all assigned tags at once. This is extremely useful for clearing specific groups of data (e.g., `Cache::tags(['people', 'artists'])->flush()`) without clearing the entire cache.

Tags let you group related cache entries and flush them together:

```php
// Store with tags
Cache::tags(['users', 'admin'])->put('user:1', $user, 600);

// Retrieve with tags
$user = Cache::tags(['users'])->get('user:1');

// Flush all entries with a tag
Cache::tags('users')->flush();
```

### Query Caching

```php
// Cache a query result
$posts = Cache::remember('posts.published', 3600, function () {
    return Post::where('published', true)
               ->with('author')
               ->orderBy('created_at', 'desc')
               ->get();
});

// Cache with user-specific key
$key = 'user.' . auth()->id() . '.dashboard';
$data = Cache::remember($key, 1800, function () {
    return Dashboard::buildFor(auth()->user());
});
```

### Cache Invalidation Strategies

**Definition:** Cache invalidation is the process of removing outdated data from the cache. Common strategies include Time-To-Live (TTL), event-driven invalidation (clearing cache when a Model is updated via Observers), or manual flushing via artisan commands.

```php
// 1. Event-based invalidation (in Observer or after model save)
class PostObserver
{
    public function saved(Post $post): void
    {
        Cache::forget('posts.published');
        Cache::forget('post.' . $post->id);
    }

    public function deleted(Post $post): void
    {
        Cache::forget('post.' . $post->id);
    }
}

// 2. Time-based (TTL) — simplest approach
Cache::put('expensive-report', $data, now()->addHours(6));

// 3. Cache versioning / cache busting
$version = Cache::get('posts.version', 1);
$posts   = Cache::remember("posts.v{$version}", 3600, fn() => Post::all());

// Bust by incrementing version
Cache::increment('posts.version');
```

### HTTP Response Caching

```php
// Cache a full response
Route::get('/reports', function () {
    return response()->json(Report::generate())
                     ->header('Cache-Control', 'public, max-age=3600');
});

// Using the cache.headers middleware
Route::middleware('cache.headers:public;max_age=3600;etag')->group(function () {
    Route::get('/static-page', [PageController::class, 'show']);
});
```

### Artisan Cache Commands

```bash
# Clear application cache
php artisan cache:clear

# Clear config cache
php artisan config:clear

# Cache config for production
php artisan config:cache

# Cache routes for production
php artisan route:cache

# Cache views for production
php artisan view:cache
```

### Best Practices

- **Use `remember()`** instead of manual `get`/`put` pairs
- **Tag related data** so you can invalidate groups efficiently
- **Keep TTLs short** for frequently changing data
- **Use Redis** in production for performance and tag support
- **Never cache sensitive data** like passwords or tokens
- **Cache at the service layer**, not inside controllers

---

## 16. Livewire

**Definition:** Livewire is a full-stack framework for Laravel that makes building dynamic interfaces simple, without leaving PHP. It renders Blade components server-side and uses AJAX under the hood to sync state between the browser and server — no custom JavaScript required for most use cases.

### Installation

```bash
composer require livewire/livewire

# Publish assets (optional)
php artisan livewire:publish --config
```

Add to your Blade layout:
```html
<!DOCTYPE html>
<html>
<head>
    @livewireStyles
</head>
<body>
    {{ $slot }}

    @livewireScripts
</body>
</html>
```

### Creating a Component

**Definition:** Livewire components differ from Blade components in that they have an associated PHP class (usually in `app/Http/Livewire`). This class holds usage state and methods that can be called directly from the frontend, enabling dynamic behavior without writing JavaScript.

```bash
php artisan make:livewire Counter
# Creates:
#   app/Livewire/Counter.php
#   resources/views/livewire/counter.blade.php
```

**Component class** (`app/Livewire/Counter.php`):
```php
<?php

namespace App\Livewire;

use Livewire\Component;

class Counter extends Component
{
    public int $count = 0;

    public function increment(): void
    {
        $this->count++;
    }

    public function decrement(): void
    {
        $this->count--;
    }

    public function render()
    {
        return view('livewire.counter');
    }
}
```

**Component view** (`resources/views/livewire/counter.blade.php`):
```html
<div>
    <h1>Count: {{ $count }}</h1>
    <button wire:click="increment">+</button>
    <button wire:click="decrement">-</button>
</div>
```

**Using in a Blade template:**
```html
<livewire:counter />
{{-- or --}}
@livewire('counter')
```

### Key Directives

**Definition:** Livewire introduces specific Blade directives to bind data and listen for events. `wire:model` binds an input to a component property (two-way binding). `wire:click` binds a click event to a component method. `wire:loading` shows elements only while an AJAX request is in flight.

| Directive | Purpose | Example |
|-----------|---------|---------|
| `wire:click` | Call a method on click | `wire:click="save"` |
| `wire:model` | Two-way data binding | `wire:model="name"` |
| `wire:model.live` | Sync on every keystroke | `wire:model.live="search"` |
| `wire:model.lazy` | Sync on blur/change | `wire:model.lazy="email"` |
| `wire:submit` | Handle form submit | `wire:submit="save"` |
| `wire:loading` | Show while request pending | `wire:loading` |
| `wire:navigate` | SPA-style navigation | `wire:navigate` |
| `wire:key` | Unique key for list items | `wire:key="item-{{ $id }}"` |

### Real-World Example: Live Search

```php
// app/Livewire/UserSearch.php
namespace App\Livewire;

use App\Models\User;
use Livewire\Component;

class UserSearch extends Component
{
    public string $search = '';

    public function render()
    {
        $users = User::when($this->search, function ($query) {
                        $query->where('name', 'like', "%{$this->search}%")
                              ->orWhere('email', 'like', "%{$this->search}%");
                    })
                    ->limit(10)
                    ->get();

        return view('livewire.user-search', compact('users'));
    }
}
```

```html
{{-- resources/views/livewire/user-search.blade.php --}}
<div>
    <input wire:model.live="search" placeholder="Search users..." />

    <ul>
        @foreach ($users as $user)
            <li>{{ $user->name }} — {{ $user->email }}</li>
        @endforeach
    </ul>

    <div wire:loading>Searching...</div>
</div>
```

### Validation

```php
class CreatePost extends Component
{
    public string $title = '';
    public string $body  = '';

    protected array $rules = [
        'title' => 'required|min:3|max:255',
        'body'  => 'required|min:10',
    ];

    public function save(): void
    {
        $validated = $this->validate();

        Post::create($validated);

        session()->flash('message', 'Post created!');
        $this->reset(['title', 'body']);
    }

    public function render()
    {
        return view('livewire.create-post');
    }
}
```

```html
<form wire:submit="save">
    <input wire:model="title" type="text" />
    @error('title') <span>{{ $message }}</span> @enderror

    <textarea wire:model="body"></textarea>
    @error('body') <span>{{ $message }}</span> @enderror

    <button type="submit">Save</button>

    @if (session()->has('message'))
        <p>{{ session('message') }}</p>
    @endif
</form>
```

### Lifecycle Hooks

**Definition:** Livewire components have lifecycle hooks similar to frontend frameworks (like Vue or React). Methods like `mount()` (initialization), `updated()` (property change), and `render()` allow you to hook into specific moments of the component's request lifecycle.

```php
class MyComponent extends Component
{
    public string $name = '';

    // Called once when component is first mounted
    public function mount(string $initialName = ''): void
    {
        $this->name = $initialName;
    }

    // Called before a property is updated
    public function updatingName(string $value): void
    {
        $this->name = strtolower($value);
    }

    // Called after a property is updated
    public function updatedName(string $value): void
    {
        // e.g., trigger a search
    }

    public function render()
    {
        return view('livewire.my-component');
    }
}
```

### Pagination

**Definition:** Livewire simplifies pagination by providing the `WithPagination` trait. Unlike standard Laravel pagination (which reloads the page), Livewire pagination reloads only the data portion of the component via AJAX, providing a smooth, SPA-like experience without writing JavaScript.

```php
use Livewire\WithPagination;

class PostList extends Component
{
    use WithPagination;

    public function render()
    {
        return view('livewire.post-list', [
            'posts' => Post::paginate(10),
        ]);
    }
}
```

```html
<div>
    @foreach ($posts as $post)
        <div>{{ $post->title }}</div>
    @endforeach

    {{ $posts->links() }}
</div>
```

### Livewire vs. Traditional AJAX

| Feature | Livewire | Traditional AJAX |
|---------|----------|-----------------|
| Language | PHP only | PHP + JavaScript |
| State management | Automatic | Manual |
| Validation | Laravel rules | Custom JS or API |
| Learning curve | Low (Laravel devs) | Medium |
| Real-time (WebSockets) | Via Echo/Pusher | Via Echo/Pusher |
| SEO | Server-rendered | Depends |

### Best Practices

- **Keep components focused** — one responsibility per component
- **Use `wire:key`** on list items to help Livewire track DOM changes
- **Debounce live search** with `wire:model.live.debounce.300ms`
- **Avoid heavy computation** in `render()` — use `Cache::remember()`
- **Use `#[Computed]` attribute** (Livewire 3) for cached computed properties
- **Protect actions** with `#[Locked]` for properties that shouldn't be modified by the client
