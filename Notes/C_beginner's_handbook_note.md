The C Beginner's Handbook: https://www.freecodecamp.org/news/the-c-beginners-handbook/?inf_contact_key=e6b96b38469cc4469ce49d9b78767df5a61f15688044e0df333a256a7a7fd2ca

THE C BEGINNER'S HANDBOOK

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

How to execute a C program

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

the compiler will raise a warning at compile time and will convert the decimal number to an float value.

C built-in data types are "int, char, short, long, float, double, long doublr". 


Integer numbers:
C provides us the following types to define integer values:

* Char
* int
* short
* long
