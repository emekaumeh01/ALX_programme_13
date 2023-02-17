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




