## The C Beginner's Handbook: https://www.freecodecamp.org/news/the-c-beginners-handbook/?inf_contact_key=e6b96b38469cc4469ce49d9b78767df5a61f15688044e0df333a256a7a7fd2ca

# THE C BEGINNER'S HANDBOOK

C is probably the most widely known programming language. It one of the popular language learnt in school aside Python and Java.

C is a low level language and sometimes regarded as an academic language

C is widely used in embedded systems and devices and powers most internet servers which are built in Linux. Infact, Linux kernal is built using C which means that C runs or powers every Andriod devices.

It was the first programming language that was portable among different OSs. Every device has a compiler that it uses to convert the C code into a machine language suitable for its Processor to execute. Which we take for granted today.

C is a compiled language like Go, Swift, Rust and Java. Which mean it convert its source program into binaries or machine code that is to be executed.

C is not garbade collected i.e you have to manage memory allocation yourself. Which becomes a complex issue but also give an advantage as it makes it idea to write programs for embedded programs and devices like Arduino.


"""C

#hello_world

#include <stdio.h>

int main(void)
{
	printf("Hello, World!");
	
	return 0
}

"""

The program first imports the stdio library which stands for ```standard input-output library```
The library gives us access to input/output functions

C is a small language at its core and some programmers have built libraries embedded in the compiler to make functions that woulddn't have been found in C's core language there by making some works easier.

```stdio``` library provides the printf() function

The function is wrapped into a main() function. The main() function is the entry point of any C program i.e where the program starts running from.

Function:
	A function is a routine that takes one or more arguments and returns a single value. In the case of main() the functions gets no arguments, and returns an integer. void keyword is used to show no argument passed and int keyword for return value.
	
The printf() function was written without a return value and has strings in it. This is called function invocation. Somewhere in the stdio printf is defined as

```C
int printf(const char *format, ...);
```

The main function we defined above will be run by the operating system when the program is executed.

## How to execute a C program

C is a compiled language and by default sometimes Linux and MacOS has in it the compiler 'gcc' already installed. You may have to run a Windows Subsystem for Linux for Windows system.

To use the compiler let's say we save our above program in a file called "hello.c". We can the use:

```bash
gcc hello.c -o hello
```

It will generate a 'hello' executable.

We can run it with:

```bash
./hello
```


Variables and Types

When you create a variable with C you have to specify the type of variable it is at the declaration. 

for example:

```C
int age
```

A varible name can contain uppercase or lowercase letters, can contain digits and the underscore character, but it can't start with a digit. 'AGE' and 'Age10' are valid variable names, '1age' is not.

You can also initialize a variable at declaration, specifying the initial value

```C
int age = 37
```

Once you declare a variacle you are then able to use it in your program code. You can change its value at any time, using "=" operator like in "age = 100"

E.g:

```C
#include <stdio.h>

int main(void)
{
	int age = 0;
	age = 37.2;
	printf("%u", age);
}

```
the compiler will raise a warning at compile time and will convert the decimal number to an float value.

C built-in data types are "int, char, short, long, float, double, long doublr". 


## Integer numbers:
C provides us the following types to define integer values:

* Char
* int
* short
* long

Most times you'll likely use an int to store an integer. But in other cased you might want to choose one of the other 3 options

The "char" type is commonly used to store letters of the ASCII chart , but it can be used to hold small integers from -128 to 127. It takes at least 1 byte. 

"int" takes at least 4 bytes. "short" takes at least 2 bytes. "long" takes at least 4 bytes.


## Unsigned Integers:

For all the above data types we can prepend "unsigned" to start the range at 0. Instead of a negative number. 

* `unsigned char` will range from 0 to at least 255
* `unsigned int` will range from 0 to at least 65,535
* `unsigned short` will range from 0 to at least 65,535
* `unsigned long` will range from 0 to at least 4, 294, 967, 295



## The problem with overflow:
	Given all those limits, a question might come up: how can we make sure our numbers do not exceed the limit? And what happens if we do exceed the limit?
	If you have an `unsigned int` number at 255, and you increment it, you'll get 256 in return. As expected. If you have `unsigned char` number at 25, and you increment it, you'll get 0 in return. It resets starting from the initial possible value.
	
If you have a `unsigned char` number at 255 and you add 10 to it, you'll get the number 9:

```C
#include <stdio.h>

int main(void){
	unsigned char j = 255;
	j = j + 10;
	printf("%u", j); /* 9 */
}

```

If you don't have a signed value, the behavior is undefined. It will basically give you a huge number which can vary, like in the case:

```C

#include <stdio.h>

int main(void)
{
	char j = 127;
	j = j + 10
	printf("%u", j); /* 473902838 */
}

```
In other words, C does not protect you fron going over the limits of a type. You need to take care of this yourself.


## Warnings when declaring the wrong type

When you declare the variable and initialize it with the wrong value, the `gcc` compiler (the one you're probably using) should warn you:

```C
#include <stdio.h>

int main(void)
{
	char j = 1000;
}

```

```bash
hello.c:4:11: warning: implicit conversion 
  from 'int' to
      'char' changes value from 1000 to -24
      [-Wconstant-conversion]
        char j = 1000;
             ~   ^~~~
1 warning generated.
```

And it also warns you in direct assignments:

```C

#include <stdio.h>

int main(void)
{
	char j;
	j = 1000;
}
```

But not if you increase the number using, for example, `+=`:

```C
#include <stdio.h>

int main(void)
{
	char j = 0;
	j += 1000;
}
```

## Foating point numbers

Floating point types can represent a much larger set of values than integers can, and can also represent fractions, something that integers can't do.

Using floating point numbers, we represent numbers as decimal numbers time powers of 10.


The following types:
* float
* double
* long double

are used to represent numbers with decimal points (floating point types). All can represent both positive and negative numbers.

The minimum requirements for nay C implementation is that `float` can represent a range between 10^-37 and 10^+37, and is typically implemented usign 32 bits. `double` can represent a bigger set of numbers. `long double` can hold even more numbers. 

The exact figures, as with integers values, depends on the implementation.

On a modern Mac, a `float` is represented in 32 bits, and has a precision of 24 significant bits. 8 bits are used to encode the exponenets

A `double` number is represented in 64 bits, with a precision of 53 significant bits. 11 bits are used to encode the exponent. The type `long double` is represented in 80 bits, has a precision of 64 significant bits. 15 bits are used to enode the exponent.

On your specific computer, how can you determine the specific size of the types? You can write a program to do that:

```C
#include <stdio.h>

int main(void)
{
	printf("char size: %lu bytes\n", sizeof(char));
	printf("int size: %lu bytes\n", sizeof(int));
	printf("short size: %lu bytes\n", sizeof(short));
	printf("long size: %lu bytes\n", sizeof(long));
	printf("float size: %lu bytes\n", sizeof(float));
	printf("double size: %lu bytes\n", sizeof(double));
	printf("long double size: %lu bytes\n", sizeof(long double));
}

```

In my system, a modern Mac, it prints:

```bash
char size: 1 bytes
int size: 4 bytes
short size: 2 bytes
long size: 8 bytes
float size: 4 bytes
double size: 8 bytes
long double size: 16 bytes
```

## Constants

A constant is declared similarly to variables, except it is prepended with the `const` keyword, and you always need to specify a value.

Like this:

```C
const int age = 37;
```

It's perfectly valid although it's common to declare constants uppercase, like this:

```C
const int AGE = 37;
```

Another way to define constants is by using this syntax:

```C
#define AGE 37
```

## Operators

C offers us a wide variety of operators that we can use to operate on data.

* arithmetic operators
* comparison operators
* logical operators
* compound assignment operators
* bitwise operators
* pointer operators
* structure operators


## Arithmetic operators
	In this macro group I am going to seperate binary operators and unary operators/
	
Binary operators work using tqo operands:

Operators || Name || Example
`=` || Assignment || `a + b`
`+` || addition || `a + b`
`-` || subtraction || `a - b`
`*` || Multiplication || `a * b`
`\` || Division || `a / b`
`%` || Modulo  || `a % b`

Unary operators only take one operand:

Operator || Name || Example
`+` || Unary plus || `+a`
`-` || Unary minus || `-a`
`++` || Increment || `a++` or `++a`
`--` || Decrement || `a--` or `--a`

The difference between a++ and ++a is that a++ increments the a variable after using it. ++a increments the a variable before using it. 

For example: 

```C
int a = 2;
int b;
b = a++; / * b is 2, a is 3 */
b = ++a; / * b is 4, a is 4 */
```

The same applies to the document operators.



## Comparison operators

Operator || Name || Example
`==` || Equal operator || `a == b`
`!=` || Not equal operator || `a != b`
`>`  || Bigger than || ` a > b`
'<'  || Less then  || `a < b`
`>=` || Bigger than or equal to || `a >= b`
`<=` || Less than or qeual to || `a <= b`


## Logical operators

* `!` NOT (example: `!a`)
* `&&` AND (example: `a && b)
* `||` OR (example: `a || b`)


## Compound assignment operators

These operators are useful to perform an assignment and at the same time perform an arithmetic operation:

Operator || Name || Example
`+=` || Addtition assignment || `a += b`
`-=` || Subtraction assignment || `a -= b`
`*=` || Multiplication assignment || `a *= b`
`/=` || Division assignment || `a /= b`
`%=` || Modulo assignment || `a %= b`


## The ternary operator

The ternary operator is the only operator in C that workswith 3 operands, and it's a short way to express conditionals

```C
<condition> ? <expression> : <expression>;
```

e.g:

```C
a ? b : c;
```

If a is evaluated to `true` then the b statement is executed, otherwise c is


## Sizeof

The `sizeof` operator return the size of the operand you pass. You can pass a variable, or even a type.

Example usage:

```C
#include <stdio.h>

int main(void)
{
	int age = 37;
	printf("%ld\n", sizeof(age));
	printf("%ld", sizeof(int));
}

```


## Operator precedence

Suppose we have this operation:

```C
int a = 2;
int b = 4;
int c = b + a * a / b - a;
```

What's the value of c?

In order from less precedence to more precedence, we have:

* the `=` assignment operator
* the `+` and `-` binary operators
* the `*` and `/` operators
* the `+` and `-` unary operators

Parentheses have higher priority over anything else.
therefore we could rewrite the expression:

```C
int c = b + ((a * a) / b) - a;
```

## Conditionals

Any programming language provides the programmers the ability to perform choices.

C provides use 2 ways to do so.

The first is the `if` statement, with its `else` helper, and the second is the `switch` statement

## If

In an `if` statement, you can check for a condition to be true, and then execute the block provided in the curly brackets:

```C
int a = 1;

if (a == 1)
{
	/* do something */
}
```

You can append an `else` block to execute a different block if the original condition turns out to be false:

```C
int a = 1;

if (a == 2)
{
	/* do something */
}
else
{
	/* do something else */
}

```

You can have multiple `else` blocks by stacking together multiple `if` statements:

```C
int a = 1;

if (a == 2)
{
	/* do something */
}
else if (a == 1)
{
	/* do something else */
}
else
{
	/* do something else again */
}
```


## switch 

If you need to do too many if/else/if block to perform a check or perhaps check the value of a number then use a `switch` statement

You can provide a variable as condition, and a series of `case` entry points for each value you expect:

```C
int a = 1;

switch (a)
{
	case 0:
		/* do something */
	break;
	case 1:
		/* do something else */
	break;
	case 2:
		/* do something else */
	break;
}
```
We need a `break` keyword at the end of each case to aviod th next case being executed when the one before ends. 

You can add a "catch-all" case at the end, labeled `default`:

```C
int a = 1;

switch (a)
{
	case 0:
		/* do something */
	break;
	case 1:
		/* do something else */
	break;
	case 2:
		/* do something else */
	break;
	default:
		/* handle all the other cases */
	break;
}
```


## Loops

C offeres us three ways to perform a loop: for loos, while loops and dp while loops. 


## For loops

Using the `for` keyword we can define the rules of loop up front, and then provide the block that is going to be executed repeatedly.

Like this:

```C
for (int i = 0; i <= 10; i++)
{
	/* instruction to be repested */
}
```

The `(int i = 0; i <= 10; i++)` block contains 3 parts of the looping details:
* the initial condition `(int i = 0)
* the test `(i <= 10)`
* the increment `i++`

This program should print `0 1 2 3 4 5 6 7 8 9 10`

```C
for (int i = 0; i <= 10; i++)
{
	/* instructions to be repeated */
	printf("%u ", i);
}
```

Loops can also start from a high number, and go a lower number.


## While loops

While loops is simpler to write than a `for` loop, because it requires a bit more work on your part. Instead of defining all the loop data up front when you start the loop, like you do in the `for` loop, using `while` you jst check for a condition.

```C
while (i < 10)
{
	/* do something */
}
```

And this loop is will be an infinite loop unless you increment the `i` variable at some point inside the loop.

The correct form of `while loop`:

```C
int i = 0;


while (i < 10)
{
	/* do something */
	i++;
}
```


## Do while loops
While loops are great, but there might be times when you need to do one particular thing: you want to always execute a block, and then maybe repeat it.

This is done using the `do while` keyword. In a way it's very similar to a `while` loop, but slightly different:

```C
int i = 0;

do {
	/* do something */
	
	i++;
} while (i < 10);

```
The block that contains the /* do something */ comments is always executed at least once, regardless of thecondition check at the bottom.

Then until `i` is less than 10, we'll repeat the block.

## Breaking out of a loop using `break`

To break out of a loop at any point in time you can use the `break` keyword. This is useful in many cases. You might want to check for the value of a varible, for example:

```C
for (int i = 0; i <= 10; i++)
{
	if (i == 4 && someVariable == 10)
	{
		break;
	}
}
```

## Arrays

An array is a variable that stores multiple values. 

Every value in the array, in C, must have the same type. This means you will have arrays of `int` values, arrays of `double` values, and more.

you can define an array of `int` values like this:

```C
int prices[5];
```

You must always specify the size of the array. C does not provide dynamic arrays out of the box ( you have to use a data structure like linked list for that).

You can use a constant to define the size:

```C
const SIZE = 5;
int prices[SIZE];
```


You can initialize an array at definition time, like this:

```C
int prices[5] = {1, 2, 3, 4, 5};
```

But you can also assign a value after the definition, in this way:


```C
int prices[5];

prices[0] = 1;
prices[1] = 2;
prices[2] = 3;
prices[3] = 4;
prices[4] = 5;
```

Or more practical, using a loop:

```C
int prices[5];

for (int 1 = 0; i < 5; i++)
{
	prices[i] = i + 1;
}
```

And you can reference an item in the array by using square brackets after the array variable name, adding an integer to determine the index value. Like this:

```C




