# Complete Guide to C# Fundamentals

**C# was developed by Microsoft**, led by **Anders Hejlsberg** and his team.

**Timeline:**
- **2000:** C# announced by Microsoft
- **2002:** C# 1.0 released with .NET Framework 1.0
- **Creator:** Anders Hejlsberg (who also created Turbo Pascal and was chief architect of Delphi)
- **Purpose:** Created as part of Microsoft's .NET initiative to compete with Java

## 1. Compilation Process: How C# Works

### Overview: C# is BOTH Compile-Time AND Runtime Language!

C# uses a **two-step compilation process**:

```
C# Source Code (.cs)
       ↓
[Compile Time - CSC Compiler]
       ↓
Intermediate Language (IL/MSIL) (.dll or .exe)
       ↓
[Runtime - JIT Compiler in CLR]
       ↓
Native Machine Code
       ↓
Execution
```

#### STEP 1: Compile-Time (Entire File at Once)

- Compiler reads **ENTIRE file(s)** at once (not line by line)
- Checks for syntax errors
- Performs type checking
- Converts to IL (Intermediate Language) / MSIL (Microsoft Intermediate Language)
- Creates assembly files (.dll or .exe)

**Example:**
```csharp
// Program.cs
int x = 10;
string name = "John";
Console.WriteLine(x + name); // Compile-time error: Cannot add int and string!
```
**Error caught at COMPILE TIME** ✓

#### STEP 2: Run-Time (JIT Compilation)

- CLR loads the IL code
- JIT compiler converts IL → Native machine code
- Code executes on the CPU
- Happens **just before execution** (hence "Just-In-Time")

**Example:**
```csharp
int[] numbers = new int[5];
Console.WriteLine(numbers[10]); // Runtime error: IndexOutOfRangeException
```
**Error caught at RUN TIME** ✗

---
## 2. Line-by-Line vs Entire File Compilation

C# compiles ENTIRE FILE(S) at once, NOT line by line

**Comparison with Other Languages:**

| Language | Compilation Style |
|----------|------------------|
| **C#** | Entire file(s) → IL → Native code |
| **Java** | Entire file(s) → Bytecode → Native code |
| **C/C++** | Entire file(s) → Native code directly |
| **Python** | Line-by-line interpretation |
| **JavaScript** | Line-by-line interpretation (with JIT) |

**Why This Matters:**
```csharp
// This works because compiler reads entire file first
public class Program
{
    static void Main()
    {
        DisplayMessage(); // Method called BEFORE definition
    }
    
    static void DisplayMessage() // Defined AFTER usage
    {
        Console.WriteLine("Hello!");
    }
}
```

If C# compiled line-by-line, this would fail! ✓

---
## 3. Platform Independence vs Dependence

C# is **PLATFORM INDEPENDENT** (with conditions)

**The Full Picture:**

```
C# Source Code (.cs) - Platform Independent
       ↓
IL Code (Intermediate Language) - Platform Independent
       ↓
.NET Runtime (CLR/CoreCLR) - Platform Dependent
       ↓
Native Machine Code - Platform Dependent
```

#### Before .NET Core (Old .NET Framework)
- **Platform Dependent** (Windows only)
- .NET Framework only worked on Windows
- Could not run on Linux/Mac natively

#### After .NET Core/.NET 5+ (Modern)
- **Platform Independent!** ✓
- Write once, run anywhere (with .NET runtime installed)
- Supports: Windows, Linux, macOS, Mobile (iOS, Android via MAUI)

**Example:**
```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine($"Running on: {Environment.OSVersion}");
        Console.WriteLine($"Platform: {Environment.Is64BitOperatingSystem}");
    }
}
```

---
## 4. Common Language Runtime (CLR)

### What is CLR?

**CLR (Common Language Runtime)** is the execution engine for .NET applications. It provides core services like memory management, security, and exception handling.

### Managed Code

Code that runs under CLR supervision:

- **CLR handles memory management** (automatic garbage collection)
- **Provides type safety** - Prevents invalid type operations
- **Security checks** - Verifies code safety before execution
- **Exception handling** - Manages runtime errors gracefully
- **Example:** C#, VB.NET code compiled to IL (Intermediate Language)

**Example of Managed Code:**
```csharp
// Managed code example - CLR handles memory automatically
string name = "John";
int age = 25;
object obj = "Hello"; // Type-safe reference

// No manual memory management needed!
// CLR's garbage collector frees memory automatically
```

### Unmanaged Code

Code that runs directly on the OS without CLR supervision:

- **Developer manages memory** - Must manually allocate/deallocate
- **No automatic garbage collection**
- **Faster but requires careful memory management**
- **Example:** C, C++ applications, Win32 API calls

**Example of Unmanaged Code:**
```csharp
// Calling unmanaged code from managed C# code
[DllImport("user32.dll")]
public static extern int MessageBox(IntPtr h, string m, string c, int type);

// Usage
MessageBox(IntPtr.Zero, "Hello", "Title", 0);
```

### Managed vs Unmanaged Comparison

| Aspect | Managed Code | Unmanaged Code |
|--------|------------|---|
| **Memory Management** | Automatic (GC) | Manual |
| **Type Safety** | Yes | No |
| **Speed** | Slightly slower | Faster |
| **Security** | High | Low |
| **Example Languages** | C#, VB.NET, F# | C, C++, Assembly |
| **Runs on** | CLR/.NET Runtime | OS directly |

---
## 5. Essential Things You MUST Know About C\#

### A. C# Language Features

1. **Strongly Typed** - Cannot mix types implicitly
2. **Object-Oriented** - Everything is an object
3. **Type-Safe** - Prevents type mismatches at compile time
4. **Managed Code** - Automatic memory management (Garbage Collection)
5. **Modern Features** - LINQ, Async/Await, Generics, Lambda expressions

### B. Compile-Time vs Runtime Errors

**Compile-Time Errors (Caught by Compiler):**
- Syntax errors
- Type mismatches
- Missing semicolons
- Undefined variables
- Access modifier violations

**Runtime Errors (Caught During Execution):**
- Division by zero
- Null reference exceptions
- Index out of range
- File not found
- Network errors

### C. Key Differences from Other Languages

| Feature | C# | Java | Python |
|---------|-----|------|--------|
| **Compilation** | IL → Native | Bytecode → Native | Interpreted |
| **Memory** | Automatic GC | Automatic GC | Automatic GC |
| **Platform** | Cross-platform | Cross-platform | Cross-platform |
| **Typing** | Static, Strong | Static, Strong | Dynamic, Strong |

---
## 6. Introduction to C\#

**POP (Procedure Oriented Programming):** Follows a step-by-step approach like an algorithm.

**OOP (Object Oriented Programming):** We create functions/methods and can call them multiple times as needed.

**Execution Flow:** POP follows a top-to-bottom flow.

**Compilation:** C# uses a **compiler** that compiles all code at once (not line-by-line like an interpreter).

**Runtime:** C# has a **Common Language Runtime (CLR)** that executes compiled code.

**File Extension:** `.cs`

### Basic Structure of C#

```csharp
class ClassName
{
    public static void Main(string[] args)
    {
        // body
    }
}
```

**Input:** `Console.ReadLine()`

**Output:** `Console.WriteLine()`

```csharp
using System;

class Program
{
	static void Main(string[] args)
	{
		Console.Write("Please enter name: ");
		string name = Console.ReadLine();

		Console.Write($"Hello {name}");
		Console.ReadKey();
	}
}
```

---
## 7. Data Types in C\#

In C#, data types are categorized into **primitive (value types)** and **non-primitive (reference types)**. Here's the key difference:

### Primitive Data Types (Value Types)

These store actual values directly in memory. When you copy a primitive variable, you create an independent copy of the value.

**Common primitive types:**

- `int`, `long`, `short`, `byte` - integers
- `float`, `double`, `decimal` - floating-point numbers
- `char` - single character
- `bool` - true/false
- `struct` - user-defined value types
- `enum` - enumeration types

```csharp
int a = 10;
int b = a;  // 'b' gets a copy of the value
b = 20;     // changing 'b' doesn't affect 'a'
// a is still 10, b is now 20
```

### Non-Primitive Data Types (Reference Types)

These store a reference (memory address) to the actual data. When you copy a reference variable, both variables point to the same object in memory.

**Common non-primitive types:**

- `string` - text (special case: immutable reference type)
- `class` - user-defined reference types
- `array` - collections of elements
- `interface` - contracts for classes
- `delegate` - method references

```csharp
int[] arr1 = {1, 2, 3};
int[] arr2 = arr1;  // 'arr2' references the same array
arr2[0] = 99;       // changing arr2 also changes arr1
// both arr1[0] and arr2[0] are now 99
```

### Key Differences

**Storage:** Primitives are stored on the stack (typically), while non-primitives are stored on the heap with references on the stack.

**Default values:** Primitives have default values (0, false, etc.), while non-primitives default to `null`.

**Performance:** Primitives are generally faster to access and use less memory overhead.

### Variables

A **variable** is used to store data.

- **Declaration:** `int a;` (reserves space for the variable)
- **Initialization:** `a = 10;` (assigns a value to the variable)

### Data Type Reference Tables

Here's a comprehensive list of C# data types with their sizes:

#### Integral Types (Integers)

|Data Type|Bytes|Bits|Range|
|---|---|---|---|
|`sbyte`|1|8|-128 to 127|
|`byte`|1|8|0 to 255|
|`short`|2|16|-32,768 to 32,767|
|`ushort`|2|16|0 to 65,535|
|`int`|4|32|-2,147,483,648 to 2,147,483,647|
|`uint`|4|32|0 to 4,294,967,295|
|`long`|8|64|-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807|
|`ulong`|8|64|0 to 18,446,744,073,709,551,615|

#### Floating-Point Types

|Data Type|Bytes|Bits|Precision|Range|
|---|---|---|---|---|
|`float`|4|32|~6-9 digits|±1.5 × 10⁻⁴⁵ to ±3.4 × 10³⁸|
|`double`|8|64|~15-17 digits|±5.0 × 10⁻³²⁴ to ±1.7 × 10³⁰⁸|
|`decimal`|16|128|28-29 digits|±1.0 × 10⁻²⁸ to ±7.9 × 10²⁸|

#### Character and Boolean Types

|Data Type|Bytes|Bits|Range/Values|
|---|---|---|---|
|`char`|2|16|U+0000 to U+FFFF (Unicode characters)|
|`bool`|1|8*|true or false|

*Note: `bool` technically uses 1 bit logically, but occupies 1 byte in memory

#### Reference Types

| Data Type   | Bytes         | Notes                                           |
| ----------- | ------------- | ----------------------------------------------- |
| `string`    | Variable      | 2 bytes per character + overhead (~20-24 bytes) |
| `object`    | Variable      | Base type for all types                         |
| `class`     | Variable      | Depends on fields/properties                    |
| `array`     | Variable      | Depends on element type and length              |
| `interface` | 8 (reference) | Reference size on 64-bit systems                |
| `delegate`  | 8 (reference) | Reference size on 64-bit systems                |

#### Special Types

|Data Type|Size|Notes|
|---|---|---|
|`IntPtr`|4 or 8|4 bytes on 32-bit, 8 bytes on 64-bit systems|
|`UIntPtr`|4 or 8|4 bytes on 32-bit, 8 bytes on 64-bit systems|
|`nint`|4 or 8|Native-sized integer (C# 9.0+)|
|`nuint`|4 or 8|Native-sized unsigned integer (C# 9.0+)|

## Quick Reference

**1 byte = 8 bits**

**Common conversions:**

- 2 bytes = 16 bits
- 4 bytes = 32 bits
- 8 bytes = 64 bits
- 16 bytes = 128 bits

**Memory tip:** Use `sizeof()` operator in C# to check the size of value types:

```csharp
Console.WriteLine(sizeof(int));     // Output: 4
Console.WriteLine(sizeof(double));  // Output: 8
Console.WriteLine(sizeof(decimal)); // Output: 16
```


```csharp
internal class Program
{
    static void Main(string[] args)
    {
        //int empid = 101;
        //String name = "kiran";
        //float empsal = 899990.0f;
        //Console.WriteLine($"name {name} salary {empsal} id {empsal}");

        int id;
        String name;
        double sal;

        id = int.Parse(Console.ReadLine());
        name = Console.ReadLine();
        sal = double.Parse(Console.ReadLine());

        Console.WriteLine($"id {id} name {name} salary {sal}");

    }
}
```

---
## 8. C# Operators

### 1. Arithmetic Operators

| Operator | Name                | Example        | Result                 |
| -------- | ------------------- | -------------- | ---------------------- |
| `+`      | Addition            | `5 + 3`        | `8`                    |
| `-`      | Subtraction         | `5 - 3`        | `2`                    |
| `*`      | Multiplication      | `5 * 3`        | `15`                   |
| `/`      | Division            | `10 / 3`       | `3` (integer division) |
| `%`      | Modulus (Remainder) | `10 % 3`       | `1`                    |
| `++`     | Increment           | `x++` or `++x` | Increases by 1         |
| `--`     | Decrement           | `x--` or `--x` | Decreases by 1         |

```csharp
int a = 5, b = 3;
Console.WriteLine(a + b);  // 8
Console.WriteLine(a % b);  // 2
```

### 2. Comparison (Relational) Operators

|Operator|Name|Example|Result|
|---|---|---|---|
|`==`|Equal to|`5 == 5`|`true`|
|`!=`|Not equal to|`5 != 3`|`true`|
|`>`|Greater than|`5 > 3`|`true`|
|`<`|Less than|`5 < 3`|`false`|
|`>=`|Greater than or equal|`5 >= 5`|`true`|
|`<=`|Less than or equal|`5 <= 3`|`false`|

```csharp
int x = 10, y = 20;
Console.WriteLine(x == y);  // false
Console.WriteLine(x < y);   // true
```

### 3. Logical Operators

|Operator|Name|Description|Example|
|---|---|---|---|
|`&&`|Logical AND|Both conditions must be true|`(5 > 3) && (8 > 5)` → `true`|
|`\|`|Logical OR|At least one condition must be true|`(5 > 3) \| (3 > 5)` → `true`|
|`!`|Logical NOT|Reverses the condition|`!(5 > 3)` → `false`|

```csharp
bool a = true, b = false;
Console.WriteLine(a && b);  // false
Console.WriteLine(a || b);  // true
Console.WriteLine(!a);      // false
```

### 4. Assignment Operators

|Operator|Example|Equivalent to|
|---|---|---|
|`=`|`x = 5`|Assigns value|
|`+=`|`x += 3`|`x = x + 3`|
|`-=`|`x -= 3`|`x = x - 3`|
|`*=`|`x *= 3`|`x = x * 3`|
|`/=`|`x /= 3`|`x = x / 3`|
|`%=`|`x %= 3`|`x = x % 3`|
|`&=`|`x &= 3`|`x = x & 3`|
|`\|=`|`x \|= 3`|`x = x \| 3`|
|`^=`|`x ^= 3`|`x = x ^ 3`|
|`<<=`|`x <<= 2`|`x = x << 2`|
|`>>=`|`x >>= 2`|`x = x >> 2`|

```csharp
int x = 10;
x += 5;  // x is now 15
x *= 2;  // x is now 30
```

### 5. Bitwise Operators

| Operator | Name        | Description                         | Example         |
| -------- | ----------- | ----------------------------------- | --------------- |
| `&`      | AND         | Sets bit to 1 if both bits are 1    | `5 & 3` → `1`   |
| `\|`     | OR          | Sets bit to 1 if any bit is 1       | `5 \| 3` → `7`  |
| `^`      | XOR         | Sets bit to 1 if bits are different | `5 ^ 3` → `6`   |
| `~`      | NOT         | Inverts all bits                    | `~5` → `-6`     |
| `<<`     | Left shift  | Shifts bits left                    | `5 << 1` → `10` |
| `>>`     | Right shift | Shifts bits right                   | `5 >> 1` → `2`  |

```csharp
int a = 5;  // 101 in binary
int b = 3;  // 011 in binary
Console.WriteLine(a & b);  // 1 (001)
Console.WriteLine(a | b);  // 7 (111)
```

### 6. Ternary (Conditional) Operator

|Operator|Syntax|Description|
|---|---|---|
|`?:`|`condition ? true_value : false_value`|Short form of if-else|

```csharp
int age = 18;
string result = (age >= 18) ? "Adult" : "Minor";
Console.WriteLine(result);  // Adult
```

### 7. Type Testing Operators

|Operator|Description|Example|
|---|---|---|
|`is`|Checks if object is of a type|`obj is string`|
|`as`|Converts type (returns null if fails)|`obj as string`|
|`typeof`|Gets Type object for a type|`typeof(int)`|
|`sizeof`|Gets size of value type in bytes|`sizeof(int)` → `4`|

```csharp
object obj = "Hello";
if (obj is string)
    Console.WriteLine("It's a string!");

string str = obj as string;  // Safe casting
```

### 8. Null-Related Operators

|Operator|Name|Description|Example|
|---|---|---|---|
|`?.`|Null-conditional|Access member only if not null|`obj?.Property`|
|`??`|Null-coalescing|Returns right if left is null|`x ?? 0`|
|`??=`|Null-coalescing assignment|Assigns if null|`x ??= 10`|
|`!`|Null-forgiving|Suppresses null warnings|`obj!.Method()`|

```csharp
string? name = null;
Console.WriteLine(name?.Length);  // No error, outputs nothing
Console.WriteLine(name ?? "Default");  // Default

int? x = null;
x ??= 5;  // x is now 5
```

### 9. Other Operators

|Operator|Name|Description|
|---|---|---|
|`.`|Member access|Access members of a type|
|`[]`|Index|Access array/collection elements|
|`()`|Method call|Invoke methods|
|`new`|Object creation|Create new instances|
|`=>`|Lambda|Define anonymous functions|
|`::`|Namespace alias|Resolve namespace conflicts|
|`?.`|Index access (null-conditional)|Safe array access|

```csharp
int[] arr = {1, 2, 3};
Console.WriteLine(arr[0]);  // 1

Func<int, int> square = x => x * x;
Console.WriteLine(square(5));  // 25
```

### 10. Operator Precedence (Highest to Lowest)

1. **Primary:** `x.y`, `x?.y`, `x?[y]`, `f(x)`, `a[i]`, `x++`, `x--`, `new`, `typeof`, `sizeof`
2. **Unary:** `+x`, `-x`, `!x`, `~x`, `++x`, `--x`, `(T)x`
3. **Multiplicative:** `*`, `/`, `%`
4. **Additive:** `+`, `-`
5. **Shift:** `<<`, `>>`
6. **Relational:** `<`, `>`, `<=`, `>=`, `is`, `as`
7. **Equality:** `==`, `!=`
8. **Logical AND:** `&`
9. **Logical XOR:** `^`
10. **Logical OR:** `|`
11. **Conditional AND:** `&&`
12. **Conditional OR:** `||`
13. **Null-coalescing:** `??`
14. **Conditional:** `?:`
15. **Assignment:** `=`, `+=`, `-=`, etc.

**Tip:** Use parentheses `()` to make your intentions clear and override default precedence!

```csharp
int result = 2 + 3 * 4;      // 14 (multiplication first)
int result2 = (2 + 3) * 4;   // 20 (parentheses first)
```

---
## 9. Type Casting in C\#

Type casting is converting a value from one data type to another. There are two main types:

### 1. Implicit Casting (Automatic)

Happens automatically when converting from a **smaller** type to a **larger** type (no data loss).

**Order:** `byte` → `short` → `int` → `long` → `float` → `double`

csharp

```csharp
int myInt = 9;
double myDouble = myInt;  // Automatic casting: int to double
Console.WriteLine(myDouble);  // 9.0

char myChar = 'A';
int charCode = myChar;  // char to int (ASCII value)
Console.WriteLine(charCode);  // 65

float myFloat = 5.5f;
double myDouble2 = myFloat;  // float to double
Console.WriteLine(myDouble2);  // 5.5
```

### 2. Explicit Casting (Manual)

Required when converting from a **larger** type to a **smaller** type (possible data loss).

csharp

```csharp
double myDouble = 9.78;
int myInt = (int)myDouble;  // Manual casting: double to int
Console.WriteLine(myInt);  // 9 (decimal part lost)

int largeNum = 300;
byte smallNum = (byte)largeNum;  // Data loss if out of range
Console.WriteLine(smallNum);  // 44 (overflow)

long myLong = 1000000;
int myInt2 = (int)myLong;
Console.WriteLine(myInt2);  // 1000000
```

```csharp
String name;
double sal;

Console.Write("Enter Name: ");
name = Console.ReadLine();
Console.Write("Enter Salary: ");
sal = double.Parse(Console.ReadLine());

double pf = sal * 0.1;

Console.WriteLine($"name {name} salary {sal} and pf is {pf}");
```

---
## 10. Decision Making - If/Else Statements 

```csharp
int pin = 1234;
double balance = 200000;

Console.Write("Enter your pin: ");
int upin = int.Parse(Console.ReadLine());

if (pin == upin)
{
    Console.Write("Enter the amount: ");
    double ubalance = double.Parse(Console.ReadLine());
    if (ubalance <= balance)
    {
        balance -= ubalance;
        Console.WriteLine($"Available Balance is {balance}");

    }
    else
    {
        Console.WriteLine("Invalid");
    }
}
else
{
    Console.WriteLine("Invalid");
}
```

---
## 11. Switch Statement (Menu-Driven)

```csharp
int choice;
Console.WriteLine("Choose one of following: \n 1.Deposit \n 2.Withdraw \n 3.Transaction \n 4.Exit");
choice = int.Parse(Console.ReadLine());
switch (choice)
{
    case 1: Console.WriteLine("Deposit");
        break;
    case 2: Console.WriteLine("Withdraw");
        break;
    case 3: Console.WriteLine("Transaction");
        break;
    default: Console.WriteLine("Invalid");
        break ;
}
```

---
## 12. Loops

### Finite Loops

```csharp
int i, sum = 0;
Console.WriteLine("Enter no: ");
int upto = int.Parse(Console.ReadLine());
for (i = 1; i <= upto; i++)
{
    sum += i;
    \\Console.WriteLine(i);
}
Console.WriteLine(sum);
```

```csharp
int i, n;
Console.WriteLine("Enter any number: ");
n=int.Parse(Console.ReadLine());
for (i = 1; i <= n; i++)
{
    if (i%2 == 0)
    {
        Console.WriteLine(i);
    }
}
```

```csharp
int n, r, sum=0;
Console.WriteLine("Enter any number: ");
n=int.Parse(Console.ReadLine());
while (n!=0)
{
    r = n % 10;
    sum += r;
    n /= 10;
}
Console.WriteLine(sum);
```

### Infinite Loops

To create an infinite loop, use one of the following patterns:

```csharp
for ( ; ; )
{
    // loop body
}

// OR

while (true)
{
    // loop body
}
```

**Control Statements:**
- `break;` - Stops the loop and exits immediately
- `continue;` - Skips the current iteration and moves to the next one

```csharp
int choice;

while (true)
{
    Console.WriteLine("Choose one of following: \n 1.Deposit \n 2.Withdraw \n 3.Transaction \n 4.Exit");
	choice = int.Parse(Console.ReadLine());
	if (choice == 1)
	{
	    Console.WriteLine("Deposit");
	}
	else if (choice == 2)
	{
	    Console.WriteLine("Withdraw");
	}
	else if (choice == 3)
	{
	    Console.WriteLine("Transaction");
	}
	else if (choice == 4) 
	{
	    break;
	}
}
```

Nested loops

```csharp
int i, j;
for(i = 1; i<= 4; i++)
{
    for(j = 1; j<= 4; j++)
    {
        Console.Write($"{i} ");
    }
    Console.WriteLine();
}
```
```terminal
1 1 1 1
2 2 2 2
3 3 3 3
4 4 4 4
```

```csharp
int i, j;
for(i = 1; i<= 4; i++)
{
    for(j = 1; j<= 4; j++)
    {
        Console.Write($"{j} ");
    }
    Console.WriteLine();
}
```
```terminal
1 2 3 4
1 2 3 4
1 2 3 4
1 2 3 4
```

```csharp
int i, j;
for(i = 1; i<= 4; i++)
{
    for(j = 1; j<= 4; j++)
    {
        Console.Write("* ");
    }
    Console.WriteLine();
}
```
```terminal
* * * *
* * * *
* * * *
* * * *
```

```csharp
int i, j;
for(i = 1; i<= 4; i++)
{
    for(j = 1; j<= i; j++)
    {
        Console.Write($" {i}");
    }
    Console.WriteLine();
}
```
```terminal
 1
 2 2
 3 3 3
 4 4 4 4
```

```csharp
int i, j;
for(i = 1; i<= 4; i++)
{
    for(j = 1; j<= i; j++)
    {
        Console.Write($" {j}");
    }
    Console.WriteLine();
}
```
```terminal
 1
 1 2
 1 2 3
 1 2 3 4
```

```csharp
int i, j;
for(i = 1; i<= 4; i++)
{
    for(j = 1; j<= i; j++)
    {
        Console.Write("* ");
    }
    Console.WriteLine();
}
```
```terminal
*
* *
* * *
* * * *
```

```csharp
int i, j;
for(i = 1; i<= 4; i++)
{
    for(j = 4; j>= i; j--)
    {
        Console.Write("* ");
    }
    Console.WriteLine();
}
```
```terminal
* * * *
* * *
* *
*
```

```csharp
int i, j;
for (i = 1; i <= 4; i++)
{
    for (j = 1; j <= i; j++)
    {
        Console.Write("* ");
    }
    Console.WriteLine();
}
for (i = 1; i<= 3; i++)
{
    for(j = 3; j>= i; j--)
    {
        Console.Write("* ");
    }
    Console.WriteLine();
}
```
```terminal
*
* *
* * *
* * * *
* * *
* *
*
```

```csharp
int i, j;
for (i = 1; i <= 4; i++)
{
    for (j = 1; j <= i; j++)
    {
        if(i % 2 == 0)
        {
            Console.Write("# ");
        }
        else
        {
            Console.Write("* ");
        }
    }
    Console.WriteLine();
}
```
```text
* 
# # 
* * * 
# # # # 
```

```csharp
int i, j;
for (i = 1; i <= 4; i++)
{
    for (j = 1; j <= i; j++)
    {
        if(j % 2 == 0)
        {
            Console.Write("# ");
        }
        else
        {
            Console.Write("* ");
        }
    }
    Console.WriteLine();
}
```
```text
*
* #
* # *
* # * #
```

---
## 13. Arrays

```csharp
int []arr = { 1, 2, 3 };

Console.WriteLine("Using for loop");
for (int i = 0; i < arr.Length; i++)
{
    Console.Write(arr[i] +" ");
}
Console.WriteLine("\nUsing foreach loop");
foreach(int x in arr)
{
    Console.Write(x +" "); 
}
```
```terminal
Using for loop
1 2 3
Using foreach loop
1 2 3
```

```csharp
int []arr = { 1, 2, 3, 4, 5, 6 };

Console.WriteLine("Display Even no's: ");
for (int i = 0; i < arr.Length; i++)
{
    if (arr[i] % 2 == 0)
    {
        Console.Write(arr[i] + " ");
    }
}

Console.WriteLine("\nDisplay Odd no's: ");
for (int i = 0; i < arr.Length; i++)
{
    if (arr[i] % 2 != 0)
    {
        Console.Write(arr[i] + " ");
    }
}
```
```terminal
Display Even no's:
2 4 6
Display Odd no's:
1 3 5
```

```csharp
char []arr = { 'a','b','c','d','e','f','g','h','i' };
char []vowels = { 'a', 'e', 'i', 'o', 'u' };
int count = 0;

for (int i = 0; i < arr.Length; i++)
{
    for(int j = 0; j < vowels.Length; j++)
    {
        if (arr[i] == vowels[j])
        {
            count++; 
        }
    }
}
Console.WriteLine(count); 
```
```terminal
3
```

### Multi-Dimensional Arrays

```csharp
int[,] marr = { {1,2,3},{4,5,6},{7,8,9} };
int r, c;
for (r = 0; r <= 2; r++)
{
    for (c = 0; c <= 2; c++)
    {
        Console.Write(marr[r, c] + " ");
    }
    Console.WriteLine();
}
foreach (int element in marr)
{
    Console.Write(element + " ");
}
```
```terminal
1 2 3
4 5 6
7 8 9
1 2 3 4 5 6 7 8 9
```

```csharp
int[] oned = new int[4];
for (int i = 0; i < oned.Length; i++)
{
    Console.Write("Enter number: ");
    oned[i] = int.Parse(Console.ReadLine());
}
Console.WriteLine("Displaying Oned array");
for (int i = 0; i < oned.Length; i++)
{
    Console.Write(oned[i] + " ");
}
```
```terminal
Enter number: 1
Enter number: 2
Enter number: 3
Enter number: 4
Displaying Array
1 2 3 4
```

```csharp
int[] arr = new int[4];
for (int i = 0; i < arr.Length; i++)
{
    Console.Write("Enter number: ");
    arr[i] = int.Parse(Console.ReadLine());
}
Console.WriteLine("Displaying Array");
for (int i = 0; i < arr.Length; i++)
{
    Console.Write(arr[i] + " ");
}
Console.WriteLine("\nSorting Array");
int temp;
for (int i = 0; i < arr.Length; i++)
{
    for (int j = i + 1; j < arr.Length; j++)
    {
        if (arr[i] > arr[j])
        {
            temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
}
Console.WriteLine("Displaying Sorted Array");
for (int i = 0; i < arr.Length; i++)
{
    Console.Write(arr[i] + " ");
}
```
```terminal
Enter number: 6
Enter number: 8
Enter number: 4
Enter number: 2
Displaying Array
6 8 4 2
Sorting Array
Displaying Sorted Array
2 4 6 8
```

```csharp
int[,] arr = new int[2, 2];
int i,j;

for(i=0; i< 2; i++)
{
    for (j=0; j< 2; j++)
    {
        Console.Write("Enter a number: ");
        arr[i,j] = int.Parse(Console.ReadLine());
    }
    Console.WriteLine();
}

Console.WriteLine("2D Array Display: ");

for (i = 0; i < 2; i++)
{
    for (j = 0; j < 2; j++)
    {
        Console.Write(arr[i,j] + " ");
    }
    Console.WriteLine();
}
```
```terminal
Enter a number: 1
Enter a number: 2

Enter a number: 3
Enter a number: 4

2D Array Display:
1 2
3 4
```

---
## 14. Object-Oriented Programming (OOP) - Fundamentals

### 1. OOP vs. POP

| Aspect | POP | OOP |
|--------|-----|-----|
| **Approach** | Top-to-Bottom | Bottom-to-Top |
| **Execution** | Line by line from main function | Main function calls classes/functions defined below |
| **Code Organization** | Procedure-based | Object/Class-based |

### 2. Class and Object

- **Class:** A blueprint or template that defines the structure and behavior of objects. It can represent any entity (e.g., Fruits, Student, Vehicle).

- **Object:** An instance (reference) of a class used to access and call its methods and properties.

### 3. Methods (Member Functions)

**Syntax:**
```csharp
access_modifier return_type MethodName(parameters)
{
    // method body
}
```

**Access Modifiers:**
- `private` - Accessible only within the specific class
- `public` - Accessible everywhere (inside and outside the class)
- `protected` - Accessible within the class and inherited (child) classes
- `internal` - Accessible within the same assembly/namespace

**Return Types:**
- `void` - Returns nothing
- Data types (`int`, `string`, `double`, etc.) - Must include a `return` statement

### 4. Static vs. Non-Static Methods

**Static Methods:**
- Defined with the `static` keyword
- No object needed to call them
- Called using: `ClassName.MethodName()` or just `MethodName()` within the class
- Can only access static data members

**Non-Static Methods:**
- No `static` keyword
- Requires an object to call them
- Called using: `objectName.MethodName()`
- Can access both static and non-static data members


**Example:**

```csharp
using System;

class Test
{
    public void DisplayNonStatic()  // Non-static method
    {
        Console.WriteLine("This is a non-static method");
    }

    public static void DisplayStatic()  // Static method
    {
        Console.WriteLine("This is a static method");
    }

    static void Main(string[] args)
    {
        // Calling non-static method (requires object)
        Test obj = new Test();
        obj.DisplayNonStatic();

        // Calling static method (no object needed)
        DisplayStatic();
        // OR: Test.DisplayStatic();
    }
}
```

**Output:**
```
This is a non-static method
This is a static method
```

```csharp
class Operations
{
    public void Display()
    {
        Console.WriteLine("This is non static method");
    }

    public void Add(int a, int b)
    {
        int sum = a + b;
        Console.WriteLine(sum);
    }

    public int Sub(double a, double b)
    {
        return (int)(a - b);
    }

    static int var = 10;

    public void NonStaticMethod()
    {
        Console.WriteLine($"Non Static Value of Var is {var}");
    }

    public static void StaticMethod()
    {
        Console.WriteLine($"Static Value of Var is {var}");
    }
}
```
```csharp
class Program
{
    static void Main(string[] args)
    {
        Operations obj1 = new Operations();
        obj1.Display();

        obj1.Add(2, 3);

        int c = obj1.Sub(3, 4);
        Console.WriteLine(c);

        obj1.NonStaticMethod(); //non-static
        Operations.StaticMethod(); //static
    }
}
```
```
This is non static method
5
-1
Non Static Value of Var is 10
Static Value of Var is 10
```

### 5. Constructors

#### Definition

- A special method used to build/initialize objects.
- load variables
- It is called automatically when an object is created.
- It must have the same name as the class and has no return type.

#### Types of Constructors

- **Default Constructor:** Parameter-less. If not defined, the system provides one by default.
- **Parameterized Constructor:** Used to load specific values into variables during object creation.
- **Copy Constructor:** Copies the instance (variables) of one constructor into another. It takes the class object as a parameter.
- **Constructor Overloading:** Having multiple constructors in a class with different signatures (parameters).

#### The this Keyword

- Used to distinguish between class fields and parameters when they share the same name.

```csharp

using Constructors;
using System;

class Program
{
    int x, y;
    public Program(int x, int y) { 
        this.x = x;
        this.y = y;
    }

    public void Display()
    {
        Console.WriteLine($"Value of x is {x} and y is {y}");
    }
    static void Main(string[] args)
    {
        Program obj = new Program(3,2);
        obj.Display();

        Copycons obj2 = new Copycons("Kiran", 101);
        Console.WriteLine("Original Constructor");
        obj2.Display2();

        Copycons obj3 = new Copycons(obj2,100000);
        Console.WriteLine("Copy Constructor");
        obj3.Display3();

        Consoverloading obj4 = new Consoverloading();
        Console.WriteLine();
        obj4.display4();

        Consoverloading obj5 = new Consoverloading(101,"kiran");
        Console.WriteLine();
        obj5.display4();

        Consoverloading obj6 = new Consoverloading(101, "kiran", 100000);
        Console.WriteLine();
        obj6.display4();

    }
}
```
```csharp
using System;

namespace Constructors
{
    internal class Copycons
    {
        String name;
        int id;
        double salary;
        public Copycons (String name, int id)
        {
            this.name = name;
            this.id = id;
        }

        public Copycons(Copycons c, double salary)
        {
            name = c.name;
            id = c.id;
            this.salary = salary;
        }

        public void Display2()
        {
            Console.WriteLine($"Name: {name}\nId: {id}");
        }
        public void Display3()
        {
            Console.WriteLine($"Name: {name}\nId: {id}\nSalary: {salary}");
        }

    }
}
```
```csharp
using System;

namespace Constructors
{
    internal class Consoverloading
    {
        String name;
        int id;
        double salary;

        public Consoverloading()
        {
            id = 0;
            name = "test";
        }
        public Consoverloading(int id, String name) { 
            this.id = id;
            this.name = name;
        }

        public Consoverloading(int id, String name, double salary)
        {
            this.id = id;
            this.name = name;
            this.salary = salary;
        }

        public void display4()
        {
            Console.WriteLine($"Id: {id}\nName: {name}\nSalary: {salary}");
        }
    }
}

```
```
Value of x is 3 and y is 2
Original Constructor
Name: Kiran
Id: 101
Copy Constructor
Name: Kiran
Id: 101
Salary: 100000

Id: 0
Name: test
Salary: 0

Id: 101
Name: kiran
Salary: 0

Id: 101
Name: kiran
Salary: 100000
```

### 6. Partial Class

**Definition:** Allows splitting a class definition across multiple files.

**Key Points:**
- All parts must use the `partial` keyword
- Useful for separating auto-generated code from custom code
- All parts are combined at compile time

**Example:**

File1.cs:
```csharp
partial class Employee
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```

File2.cs:
```csharp
partial class Employee
{
    public void DisplayInfo()
    {
        Console.WriteLine($"Name: {Name}, Age: {Age}");
    }
}
```

**Usage (both files combined at compile time):**
```csharp
Employee emp = new Employee();
emp.Name = "John";
emp.Age = 30;
emp.DisplayInfo();
```

**Use Cases:**
- Separating designer-generated code (like Windows Forms)
- Working with large classes split across team members
- Organizing code logically
- Keeping generated code separate from manual code

---
## 15. Object-Oriented Programming (OOP) - The 4 Pillars

OOP has **4 fundamental pillars**:

1. **Inheritance**
2. **Polymorphism**
3. **Encapsulation**
4. **Abstraction**

### 1. Inheritance

#### 1. Concept

- A mechanism to maintain relationships between classes (parent/child) allowing code reusability.
- **Syntax:** `ChildClass : ParentClass`

#### 2. Types of Inheritance Supported in C#

- **Single Inheritance:** One parent → One child
- **Multilevel Inheritance:** Parent → Child → GrandChild (e.g., A → B → C)
- **Hierarchical Inheritance:** One parent → Multiple child classes
- **Note:** Multiple and Hybrid inheritance are not directly supported due to ambiguity

#### 3. The base Keyword

- Used in a child class to access members (methods/constructors) of the parent class directly

##### Single Inheritance

```csharp
using System;

class Parent
{
    int a = 2;
    
    public void DisplayParent()
    {
        Console.WriteLine("Parent class");
    }
    
    public void DisplayParent2()
    {
        Console.WriteLine($"Parent class {a}");
    }
}

class Child : Parent
{
    public void DisplayChild()
    {
        base.DisplayParent2();
        Console.WriteLine("Child class");
    }
}
```

**Main Program:**

```csharp
class Program
{
    static void Main(string[] args)
    {
        Child obj = new Child();
        obj.DisplayChild();
        obj.DisplayParent();
    }
}
```

**Output:**
```
Parent class 2
Child class
Parent class
```

##### Multilevel Inheritance

```csharp
using System;

class GrandParent
{
    public void DisplayGrandParent()
    {
        Console.WriteLine("GrandParent class");
    }
}

class Parent : GrandParent
{
    public void DisplayParent()
    {
        base.DisplayGrandParent();
        Console.WriteLine("Parent class");
    }
}

class Child : Parent
{
    public void DisplayChild()
    {
        base.DisplayParent();
        Console.WriteLine("Child class");
    }
}
```

**Main Program:**

```csharp
class Program
{
    static void Main(string[] args)
    {
        Child obj = new Child();
        obj.DisplayChild();
    }
}
```

**Output:**
```
GrandParent class
Parent class
Child class
```

##### Hierarchical Inheritance

```csharp
using System;

class Parent
{
    public void DisplayParent()
    {
        Console.WriteLine("Parent class");
    }
}

class Child1 : Parent
{
    public void DisplayChild()
    {
        base.DisplayParent();
        Console.WriteLine("Child class 1");
    }
}

class Child2 : Parent
{
    public void DisplayChild()
    {
        base.DisplayParent();
        Console.WriteLine("Child class 2");
    }
}
```

**Main Program:**

```csharp
class Program
{
    static void Main(string[] args)
    {
        Child1 obj1 = new Child1();
        obj1.DisplayChild();

        Child2 obj2 = new Child2();
        obj2.DisplayChild();
    }
}
```

**Output:**
```
Parent class
Child class 1
Parent class
Child class 2
```

### 2. Polymorphism

#### 1. Why Multiple and Hybrid Inheritance Fail

- **Ambiguity Issue:** If two parent classes have a method with the same name, the child class won't know which one to call. This creates a **"Diamond Problem"** or ambiguity.

#### 2. Types of Polymorphism

- **Compile-time Polymorphism (Method Overloading):** Multiple functions with the same name but different signatures (different parameters) within the same class. Also called **Early Binding** or **Static Binding**.
- **Runtime Polymorphism (Method Overriding):** Multiple functions with the same name and same signature in different classes (parent/child). Requires `virtual` and `override` keywords. Also called **Late Binding** or **Dynamic Binding**.

#### Method Overloading

```csharp
using System;

internal class Overload
{
    public void Display()
    {
        Console.WriteLine("This is a simple display");
    }
    
    public void Display(int id)
    {
        Console.WriteLine($"This displays ID: {id}");
    }
    
    public void Display(string name)
    {
        Console.WriteLine($"This displays Name: {name}");
    }
    
    public void Display(string address, double salary)
    {
        Console.WriteLine($"This displays Address: {address} & Salary: {salary}");
    }
}
```

**Main Program:**

```csharp
class Program
{
    static void Main(string[] args)
    {
        Overload obj = new Overload();
        obj.Display();
        obj.Display(101);
        obj.Display("kiran");
        obj.Display("mumbai", 1000000);
    }
}
```

**Output:**
```
This is a simple display
This displays ID: 101
This displays Name: kiran
This displays Address: mumbai & Salary: 1000000
```

#### Method Overriding

- **`virtual`** - Written in parent class methods indicating the method can be overridden
- **`override`** - Written in child class indicating that it is overriding the parent class method

**Simple Example:**

```csharp
using System;

class Parent
{
    public virtual void Display()
    {
        Console.WriteLine("This is parent method");
    }
}

class Child : Parent
{
    public override void Display()
    {
        Console.WriteLine("This is child method");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Child obj = new Child();
        obj.Display();
    }
}
```

**Output:**
```
This is child method
```

**Complex Example with Employee Classes:**

```csharp
using System;

// Base class
public class Employee
{
    protected string name;
    protected int id;
    protected decimal baseSalary;

    // Constructor
    public Employee(string name, int id, decimal baseSalary)
    {
        this.name = name;
        this.id = id;
        this.baseSalary = baseSalary;
        Console.WriteLine($"Employee constructor called for {name}");
    }

    // Virtual method - can be overridden
    public virtual decimal CalculateSalary()
    {
        return baseSalary;
    }

    // Virtual method for displaying info
    public virtual void DisplayInfo()
    {
        Console.WriteLine($"ID: {id}, Name: {name}, Base Salary: ${baseSalary:N2}");
    }
}

// Derived class 1
public class Manager : Employee
{
    private decimal bonus;
    private int teamSize;

    // Constructor calling base constructor
    public Manager(string name, int id, decimal baseSalary, decimal bonus, int teamSize) 
        : base(name, id, baseSalary)
    {
        this.bonus = bonus;
        this.teamSize = teamSize;
        Console.WriteLine($"Manager constructor called");
    }

    // Override the CalculateSalary method
    public override decimal CalculateSalary()
    {
        // Call base method and add bonus
        return base.CalculateSalary() + bonus + (teamSize * 500);
    }

    // Override DisplayInfo method
    public override void DisplayInfo()
    {
        base.DisplayInfo();
        Console.WriteLine($"Role: Manager, Team Size: {teamSize}, Bonus: ${bonus:N2}");
        Console.WriteLine($"Total Salary: ${CalculateSalary():N2}");
    }
}

// Derived class 2
public class Developer : Employee
{
    private string programmingLanguage;
    private int projectsCompleted;

    // Constructor
    public Developer(string name, int id, decimal baseSalary, string language, int projects) 
        : base(name, id, baseSalary)
    {
        this.programmingLanguage = language;
        this.projectsCompleted = projects;
        Console.WriteLine($"Developer constructor called");
    }

    // Override CalculateSalary
    public override decimal CalculateSalary()
    {
        // Add project bonus
        decimal projectBonus = projectsCompleted * 1000;
        return base.CalculateSalary() + projectBonus;
    }

    // Override DisplayInfo
    public override void DisplayInfo()
    {
        base.DisplayInfo();
        Console.WriteLine($"Role: Developer, Language: {programmingLanguage}");
        Console.WriteLine($"Projects Completed: {projectsCompleted}");
        Console.WriteLine($"Total Salary: ${CalculateSalary():N2}");
    }
}

// Main program
class Program
{
    static void Main()
    {
        Console.WriteLine("=== Creating Employees ===\n");

        // Create different employee types
        Employee emp = new Employee("John Doe", 101, 50000);
        Manager mgr = new Manager("Jane Smith", 102, 70000, 10000, 5);
        Developer dev = new Developer("Bob Johnson", 103, 60000, "C#", 12);

        Console.WriteLine("\n=== Employee Information ===\n");

        emp.DisplayInfo();
        Console.WriteLine();

        mgr.DisplayInfo();
        Console.WriteLine();

        dev.DisplayInfo();

        Console.WriteLine("\n=== Polymorphism Example ===\n");

        // Array of Employee references
        Employee[] employees = { emp, mgr, dev };

        foreach (var employee in employees)
        {
            Console.WriteLine($"{employee.GetType().Name} Salary: ${employee.CalculateSalary():N2}");
        }
    }
}
```

**Output:**
```
=== Creating Employees ===

Employee constructor called for John Doe
Employee constructor called for Jane Smith
Manager constructor called
Employee constructor called for Bob Johnson
Developer constructor called

=== Employee Information ===

ID: 101, Name: John Doe, Base Salary: $50,000.00

ID: 102, Name: Jane Smith, Base Salary: $70,000.00
Role: Manager, Team Size: 5, Bonus: $10,000.00
Total Salary: $82,500.00

ID: 103, Name: Bob Johnson, Base Salary: $60,000.00
Role: Developer, Language: C#
Projects Completed: 12
Total Salary: $72,000.00

=== Polymorphism Example ===

Employee Salary: $50,000.00
Manager Salary: $82,500.00
Developer Salary: $72,000.00
```

### 3. Encapsulation & Sealed Keyword

#### 1. Sealed Keyword

- **On Variables:** Prevents value changes (Constant)
- **On Methods:** Prevents method overriding
- **On Classes:** Prevents inheritance (cannot derive from a sealed class)

#### 2. Encapsulation

- **Definition:** Wrapping data (variables) and methods into a single unit to secure data
- **Implementation:** Make variables private and access them via public getter and setter methods

#### 3. Auto-Implemented Properties

- Short-hand syntax in C# to create properties without manually defining private fields

**Example:**

```csharp
class Employee
{
    public int ID { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
    public double Salary { get; set; }
}
```

**Main Program:**

```csharp
using System;

class Program
{
    static void Main()
    {
        Employee obj = new Employee();

        obj.ID = 1;
        obj.Name = "Kiran";
        obj.Age = 22;
        obj.Salary = 10000.00;

        Console.WriteLine(obj.ID);
        Console.WriteLine(obj.Name);
        Console.WriteLine(obj.Age);
        Console.WriteLine(obj.Salary);
    }
}
```

**Output:**
```
1
Kiran
22
10000
```

### 4. Abstraction

**Definition:** Hiding internal implementation details and showing only essential features to the user.

**Implementation:** Achieved via interfaces or abstract classes.

#### 1. Interfaces

- Achieves **100% abstraction**
- Contains only abstract methods (no body) by default
- Used to achieve multiple inheritance in C#
- **Syntax:** `interface InterfaceName`
- Methods are public by default
- A class implements an interface using `:` and must provide definitions for all methods
- Can contain only abstract methods (no body, must be overridden); non-abstract methods (with body) are not allowed

**Simple Interface Example:**

```csharp
using System;

interface MyInterface
{
    void DisplayMethod1();
    void DisplayMethod2();
}

class ImplementsClass : MyInterface
{
    public void DisplayMethod1()
    {
        Console.WriteLine("This is method 1");
    }

    public void DisplayMethod2()
    {
        Console.WriteLine("This is method 2");
    }
}

class Program
{
    static void Main(string[] args)
    {
        ImplementsClass obj = new ImplementsClass();
        obj.DisplayMethod1();
        obj.DisplayMethod2();
    }
}
```

**Output:**
```
This is method 1
This is method 2
```

**Multiple Interface Inheritance Example:**

```csharp
interface Interface1
{
    void Interface1Method();
}

interface Interface2
{
    void Interface2Method();
}

interface Interface3 : Interface1, Interface2
{
    void Interface3Method();
}

using System;

class ImplClass : Interface3
{
    public void Interface1Method()
    {
        Console.WriteLine("Interface 1 Method");
    }

    public void Interface2Method()
    {
        Console.WriteLine("Interface 2 Method");
    }

    public void Interface3Method()
    {
        Console.WriteLine("Interface 3 Method");
    }
}

class Program
{
    static void Main(string[] args)
    {
        ImplClass obj = new ImplClass();
        obj.Interface1Method();
        obj.Interface2Method();
        obj.Interface3Method();
    }
}
```

**Output:**
```
Interface 1 Method
Interface 2 Method
Interface 3 Method
```

**Combining Class and Interface:**

```csharp
interface OneInterface
{
    void DisplayInterface();
}

class OneClass
{
    public void DisplayClass()
    {
        Console.WriteLine("I am a class method");
    }
}

class ClassInterfaceImplements : OneClass, OneInterface
{
    public void DisplayInterface()
    {
        Console.WriteLine("I am an interface method");
    }
}

using System;

class Program
{
    static void Main(string[] args)
    {
        ClassInterfaceImplements obj = new ClassInterfaceImplements();
        obj.DisplayClass();
        obj.DisplayInterface();
    }
}
```

**Output:**
```
I am a class method
I am an interface method
```

#### 2. Abstract Class

- Defined with `abstract` keyword
- Can achieve **0% to 100% abstraction**
- Can contain both abstract methods (no body, must be overridden) and non-abstract methods (with body)
- **Object Creation:** You cannot create an object of an abstract class, but you can create a reference to it

**Example with Abstract and Non-Abstract Methods:**

```csharp
using System;

abstract class MyAbstract
{
    public abstract void Display1(); // Abstract method - no body

    public void Display2() // Non-abstract method - with body
    {
        Console.WriteLine("This is display of non-abstract method");
    }
}

class ImplementClass : MyAbstract
{
    public override void Display1()
    {
        Console.WriteLine("This is display of abstract method");
    }
}

class Program
{
    static void Main(string[] args)
    {
        // MyAbstract obj = new MyAbstract(); // Cannot instantiate abstract class
        
        // Create reference of abstract class pointing to derived class
        MyAbstract obj;
        obj = new ImplementClass();

        obj.Display1();
        obj.Display2();
    }
}
```

**Output:**
```
This is display of abstract method
This is display of non-abstract method
```

**Real-World Example - Geometric Shapes:**

```csharp
using System;

abstract class MyAbstract
{
    public abstract double Calculate(double x);
}

class Square : MyAbstract
{
    public override double Calculate(double x)
    {
        double area = x * x;
        return area;
    }
}

class AreaCircle : MyAbstract
{
    public override double Calculate(double x)
    {
        double area = 3.14 * x * x;
        return area;
    }
}

class Program
{
    static void Main(string[] args)
    {
        MyAbstract obj; // Declaration

        obj = new Square(); // Reference to Square
        double areaSquare = obj.Calculate(2.5);
        Console.WriteLine($"Area of square is {areaSquare}");

        obj = new AreaCircle(); // Reference to AreaCircle
        double areaCircle = obj.Calculate(2.5);
        Console.WriteLine($"Area of circle is {areaCircle}");
    }
}
```

**Output:**
```
Area of square is 6.25
Area of circle is 19.625
```

---
## 16. Exception Handling

### 1. Concept

- **Definition:** Handling run-time errors (logical errors) to prevent the application from crashing or stopping abruptly
- **Common Examples:** Division by zero, array index out of bounds

#### 2. Exception Blocks

- **Try:** Contains the code that might cause an error
- **Catch:** Catches the exception if one occurs. Can handle specific exception classes like `DivideByZeroException` or the generic `Exception` class
- **Finally:** Executes regardless of whether an exception occurred or not (used for cleanup)
- **Throw:** Used to raise custom exceptions

#### 3. System Exceptions (Built-in)

- `NullReferenceException` - Accessing null object
- `IndexOutOfRangeException` - Invalid array index
- `DivideByZeroException` - Division by zero
- `FileNotFoundException` - File not found
- `InvalidCastException` - Invalid type conversion
- `ArgumentException` - Invalid argument passed

**Example 1 - Division by Zero:**

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        int a = 2, b = 0, c;
        try
        {
            c = a / b;
            Console.WriteLine(c);
        }
        catch (Exception e)
        {
            Console.WriteLine(e);
        }
        finally
        {
            Console.WriteLine("Code executed successfully");
        }
    }
}
```

**Output:**
```
System.DivideByZeroException: Attempted to divide by zero.
   at Program.Main(String[] args) in C:\Users\Admin\source\repos\ExceptionHandling\ExceptionHandling\Program.cs:line 9
Code executed successfully
```

**Example 2 - Multiple Exception Handling:**

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        int a = 2, b = 2, c;
        int[] arr = new int[5];
        try
        {
            c = a / b;
            Console.WriteLine(c);
            arr[7] = 30; // Index out of range
            Console.WriteLine(arr[7]);
        }
        catch (DivideByZeroException e)
        {
            Console.WriteLine(e);
        }
        catch (Exception e1)
        {
            Console.WriteLine(e1);
        }
        finally
        {
            Console.WriteLine("Code executed successfully");
        }
    }
}
```

**Output:**
```
1
System.IndexOutOfRangeException: Index was outside the bounds of the array.
   at Program.Main(String[] args) in C:\Users\Admin\source\repos\ExceptionHandling\ExceptionHandling\Program.cs:line 12
Code executed successfully
```

#### 4. Custom Exceptions

Creating user-defined exception logic (e.g., voting age validation or insufficient bank funds).

**Example - Custom Age Exception:**

```csharp
using System;

class InvalidAgeException : Exception
{
    public InvalidAgeException()
    {
        Console.WriteLine("Invalid Age Exception");
    }
}

class CustomException
{
    public void CheckException()
    {
        int age;
        Console.Write("Enter Age: ");
        age = int.Parse(Console.ReadLine());
        try
        {
            if (age < 18)
            {
                throw new InvalidAgeException();
            }
            else
            {
                Console.WriteLine("You are eligible for voting");
            }
        }
        catch (InvalidAgeException e)
        {
            // Handle custom exception
        }
        finally
        {
            Console.WriteLine("Executed custom exception code successfully");
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        CustomException obj = new CustomException();
        obj.CheckException();
    }
}
```

**Output:**
```
Enter Age: 17
Invalid Age Exception
Executed custom exception code successfully
```

---