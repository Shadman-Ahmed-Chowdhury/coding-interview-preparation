# PHP Technical Notes
This directory contains my personal notes and resources related to PHP programming. It covers various aspects of PHP, including syntax, functions, best practices, and common use cases.

## Contents

- [Introduction to PHP](#introduction-to-php)
    - [What is PHP?](#what-is-php)
- [PHP Syntax and Basics](#php-syntax-and-basics)
    - [PHP Loops Example](#php-loops-example)
    - [PHP Conditional Statements Example](#php-conditional-statements-example)
    - [PHP Return Declare and Tickable Statements](#php-return-declare-and-tickable-statements)
    - [How to include files in PHP](#how-to-include-files-in-php)
    - [PHP Heredoc and Nowdoc](#php-heredoc-and-nowdoc)
    - [PHP type hints for functions](#php-type-hints-for-functions)
        - [The mixed type](#the-mixed-type)
    - [PHP Strict Types](#php-strict-types)
- [Working with Functions](#working-with-functions)
- [Object-Oriented PHP](#object-oriented-php)
- [PHP Best Practices](#php-best-practices)
- [Common PHP Use Cases](#common-php-use-cases)

## Introduction to PHP


### What is PHP?
PHP (Hypertext Preprocessor) is a popular server-side scripting language designed for web development. It is widely used for creating dynamic web pages and applications.

Further read: https://www.phptutorial.net/php-tutorial/what-is-php/
Video tutorial: https://www.youtube.com/watch?v=sVbEyFZKgqk

[Back To Top ⬆️](#contents)

## PHP Syntax and Basics

PHP syntax is similar to C and Perl. It uses a combination of HTML and PHP code to create dynamic web content. Here are some key points about PHP syntax:

- PHP code is embedded within HTML using `<?php ... ?>` tags.
- Variables are declared with a `$` sign, e.g., `$variableName`.
- PHP supports various data types, including strings, integers, arrays, and objects.
- Control structures like `if`, `else`, `while`, and `for` are used for flow control.

```php
<?php
// This is a single-line comment

/*
This is a multi-line comment
*/

$greeting = "Hello, World!";
echo $greeting;
?>
```
[Back To Top ⬆️](#contents)

### PHP Loops Example

```php
<?php
for ($i = 0; $i < 5; $i++) {
    echo "Iteration: " . $i . "\n";
}
?>
```

[Back To Top ⬆️](#contents)

### PHP Conditional Statements Example

```php
<?php
$number = 10;

if ($number > 0) {
    echo "The number is positive.";
} elseif ($number < 0) {
    echo "The number is negative.";
} else {
    echo "The number is zero.";
}
?>
```
[Back To Top ⬆️](#contents)

### PHP Return Declare and Tickable Statments

In PHP, the `declare` construct is used to set execution directives for a block of code. One of its most common uses is to enable tickable statements, which allow you to register functions that will be called on each tick (a tick is an event that occurs at certain points during the execution of a script).

Tickable statements can be useful for debugging, profiling, or implementing custom behavior during script execution.

Declare strict types:
what is declare strict types in php
    In PHP, the `declare(strict_types=1);` directive is used to enable strict type checking for function arguments and return values. When strict types are enabled, PHP will throw a TypeError if a value of the wrong type is passed to a function or returned from a function.

```php
<?php
declare(ticks=1);
function tick_handler() {
    echo "Tick handler called!\n";
}
register_tick_function('tick_handler');

for ($i = 0; $i < 3; $i++) {
    echo "Loop iteration: $i\n";
    sleep(1); // Simulate some work
}
?>
```
[Back To Top ⬆️](#contents)

### How to include files in PHP
In PHP, you can include files using the `include`, `include_once`, `require`, and `require_once` statements. These statements allow you to reuse code across multiple files.

```php
<?php
include 'header.php'; // Includes the file and continues execution even if the file is not found
require 'config.php'; // Includes the file and halts execution if the file is not found
?>
```

I want to get the contents of the file as a string
```php
<?php
ob_start();
include_once 'nav.php';
$nav = ob_get_clean();
echo $nav;
?>
```
[Back To Top ⬆️](#contents)


### PHP Heredoc and Nowdoc
🧩 Heredoc and Nowdoc in PHP

Heredoc (<<<) and Nowdoc (<<<' ') are used to define multi-line strings easily — especially useful for SQL queries or long text blocks.

🔹 Heredoc

Works like double quotes (" ") → variables and escape sequences are parsed.

Starts with <<<IDENTIFIER and ends with the same IDENTIFIER (must be at the start of the line).

Example:
```php
$userId = 5;

$sql = <<<SQL
SELECT id, name, email
FROM users
WHERE id = $userId
AND status = 'active';
SQL;

echo $sql;
```

✅ Output:
```
SELECT id, name, email
FROM users
WHERE id = 5
AND status = 'active';
```
🔹 Nowdoc

Works like single quotes (' ') → variables are not parsed.

Useful when you want the string to remain literal.

Example:
```php
$userId = 5;

$sql = <<<'SQL'
SELECT id, name, email
FROM users
WHERE id = $userId
AND status = 'active';
SQL;

echo $sql;
```

✅ Output:
```
SELECT id, name, email
FROM users
WHERE id = $userId
AND status = 'active';
```

🧠 Summary
Feature	Heredoc	Nowdoc
Variable parsing	✅ Yes	❌ No
Acts like	Double quotes	Single quotes
Use case	Dynamic SQL / text	Static SQL / template


[Back To Top ⬆️](#contents)

### PHP type hints for functions

Type hints allow you to specify the expected data types of function arguments and return values. This helps catch errors early and improves code readability.

#### Example of Type Hinting

```php
<?php
function add(int $a, int $b): int {
    return $a + $b;
}

$result = add(5, 10);
echo $result; // Outputs: 15
?>
```

#### The mixed type
The `mixed` type hint indicates that a parameter or return value can be of any type. This is useful when a function needs to handle multiple types of data.
The mixed type is equivalent to the following union type:

> object|resource|array|string|int|float|bool|null

```php
<?php
function processData(mixed $data): void {
    if (is_array($data)) {
        echo "Processing an array with " . count($data) . " elements.\n";
    } elseif (is_string($data)) {
        echo "Processing a string: $data\n";
    }
}
```

> Note:
`To make a type nullable, prefix the type with a question mark (?type).`

[Back To Top ⬆️](#contents)

### PHP Strict Types
To enable strict typing, you can use the declare(strict_types=1); directive at the beginning of the file like this:
```php
<?php

declare(strict_types=1);

function add(int $x, int $y)
{
    return $x + $y;
}

echo add(1.5, 2.5); 
```
By adding the strict typing directive to the file, the code will execute in strict mode. PHP enables the strict mode on a per-file basis.

In the strict mode, PHP expects the values with the type to match the target types. If there’s a mismatch, PHP will issue an error.

If you execute the script again, PHP will issue an error as follows:
```
Fatal error: Uncaught TypeError: Argument 1 passed to add() must be of the type 
```
[Back To Top ⬆️](#contents)

## Working with Functions

Functions are a fundamental building block in PHP. They allow you to encapsulate code for reusability and better organization. Here are some key points about working with functions in PHP:

- Functions are defined using the `function` keyword.
- You can pass parameters to functions and return values.
- PHP has many built-in functions, and you can also create your own.

```php
<?php
function add($a, $b) {
    return $a + $b;
}

$result = add(5, 10);
echo $result; // Outputs: 15
?>