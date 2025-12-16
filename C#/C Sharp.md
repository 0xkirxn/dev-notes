## Introduction to C Sharp

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


## Data Types in C#

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

## Key Differences

**Storage:** Primitives are stored on the stack (typically), while non-primitives are stored on the heap with references on the stack.

**Default values:** Primitives have default values (0, false, etc.), while non-primitives default to `null`.

**Performance:** Primitives are generally faster to access and use less memory overhead.
A **variable** is used to store data.

- **Declaration:** `int a;` (reserves space for the variable)
- **Initialization:** `a = 10;` (assigns a value to the variable)

Here's a comprehensive list of C# data types with their sizes:

## Integral Types (Integers)

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

## Floating-Point Types

|Data Type|Bytes|Bits|Precision|Range|
|---|---|---|---|---|
|`float`|4|32|~6-9 digits|±1.5 × 10⁻⁴⁵ to ±3.4 × 10³⁸|
|`double`|8|64|~15-17 digits|±5.0 × 10⁻³²⁴ to ±1.7 × 10³⁰⁸|
|`decimal`|16|128|28-29 digits|±1.0 × 10⁻²⁸ to ±7.9 × 10²⁸|

## Character and Boolean Types

|Data Type|Bytes|Bits|Range/Values|
|---|---|---|---|
|`char`|2|16|U+0000 to U+FFFF (Unicode characters)|
|`bool`|1|8*|true or false|

*Note: `bool` technically uses 1 bit logically, but occupies 1 byte in memory

## Reference Types

| Data Type   | Bytes         | Notes                                           |
| ----------- | ------------- | ----------------------------------------------- |
| `string`    | Variable      | 2 bytes per character + overhead (~20-24 bytes) |
| `object`    | Variable      | Base type for all types                         |
| `class`     | Variable      | Depends on fields/properties                    |
| `array`     | Variable      | Depends on element type and length              |
| `interface` | 8 (reference) | Reference size on 64-bit systems                |
| `delegate`  | 8 (reference) | Reference size on 64-bit systems                |

## Special Types

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

## C# Operators

## 1. Arithmetic Operators

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

## 2. Comparison (Relational) Operators

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

## 3. Logical Operators

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

## 4. Assignment Operators

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

## 5. Bitwise Operators

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

## 6. Ternary (Conditional) Operator

|Operator|Syntax|Description|
|---|---|---|
|`?:`|`condition ? true_value : false_value`|Short form of if-else|

```csharp
int age = 18;
string result = (age >= 18) ? "Adult" : "Minor";
Console.WriteLine(result);  // Adult
```

## 7. Type Testing Operators

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

## 8. Null-Related Operators

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

## 9. Other Operators

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

## 10. Operator Precedence (Highest to Lowest)

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

## Type Casting in C#

Type casting is converting a value from one data type to another. There are two main types:

## 1. Implicit Casting (Automatic)

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

## 2. Explicit Casting (Manual)

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

## Decision Making - If/Else Statements 

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

## Switch Statement (Menu-Driven)

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

## Loops

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
```terminal
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

## Arrays

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

## Object-Oriented Programming (OOP) Concepts

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

### Constructors

1. Definition

- A special method used to build/initialize objects.
- load variables
- It is called automatically when an object is created.
- It must have the same name as the class and has no return type.

2. Types of Constructors

- Default Constructor: Parameter-less. If not defined, the system provides one by default.
- Parameterized Constructor: Used to load specific values into variables during object creation.
- Copy Constructor: Copies the instance (variables) of one constructor into another. It takes the class object as a parameter.
- Constructor Overloading: Having multiple constructors in a class with different signatures (parameters).

3. The this Keyword

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

## Object-Oriented Programming (OOP)

OOP has **4 fundamental pillars**:

1. **Inheritance**
2. **Polymorphism**
3. **Encapsulation**
4. **Abstraction**

### Inheritance

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