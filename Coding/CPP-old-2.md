# Basics
You need to put `;` after most of the lines  

## Hello world
``` C++
#include <iostream>

int main(){
    std::cout << "Hello World!" << std::endl;
    return 0;
}
```

`#include <iostream>` importing 3rd-party library, for example this one works with console  
`int main(){}` main function in C++, runs whole time  
`std::cout <<` prints following text in console  
`"Hello World!"` text to print  
`<< std::endl;` newline - it this wasn't here, another *std::cout* will still be on the same line as previous text. You can also use `"Hello World!\n" `  
`return 0;` tells the OS that everything run successfully, but it's not necessary

## Comments
``` C++
#include <iostream>

// Comment here
// using namespace std;

int main(){
    std::cout << "Hello World!" << std::endl;
    /* 
        Multiline
        comment
        here
    */ 
    return 0;
}
```

Comments are ignored by compiler. They are used for developers to better understand something  
You can't nest comments - put a comment inside another one, it will bring you error 

## Errors and Warnings
- Compiler Time Errors
    - Program isn't going to compile, you won't get *.exe* file
    - You have to go back, fix this problem and compile again to run file
    - These include:
        - Missing semicolons
- Runtime Errors
    - Compile was successfull, but the program ins't doing what you wanted to
    - Basically some logical error
    - Sometimes they can cause the program to crash
- Warnings
    - Not serious for the compiler
    - Compilation is going to succeed, but the compiler is telling you that you are doing something that has problem, and you should fix it before it turns into serious problem
    - These include:
        - Division by 0

## Statements and Functions
**Statement** is a basic unit of computation in a C++ program. Statements end with a **semicolon**  
**Function** are reusable pieces of code, that group together a bunch of statements to do whatever we want to do. We can call them multiple times without writing similar statements over and over

``` C++
#include <iostream>

// Function
int addNumbers(int first_number, int second_number){
    int sum = first_number + second_number; 
    return sum;
}

int main(){

    int firstNumber = 12; // Statement
    int secondNumber = 9; 
    int sum1 = firstNumber + secondNumber; 

    // Calling a function
    int sum2 = addNumbers(7, 19); 

    std::cout << "The 1st sum is : " << sum1 << std::endl;
    std::cout << "The 2nd sum is : " << sum2 << std::endl;
    std::cout << "The 3rd sum is : " << addNumbers(4, 15) << std::endl;
    
    return 0;
}
```

## Input and Output
### Input
Similarly like `std::cout << name`, you can use `std::cin >> name` to **get input** and store it as *name* variable

``` C++
#include <iostream>

int main(){

    std::string name;
    int age;

    std::cout << "Enter your first name: ";
    std::cin >> name;

    std::cout << "Enter your age: ";
    std::cin >> age;

    std::cout << "Hello " << name << "!" << std::endl;
    std::cout << "You are " << age << " years old!" << std::endl;

    return 0;
}
```

You can also input **multiple variables** at the same time, but they need to be separated with a whitespace
``` C++
    std::cout << "Enter your first name and age, separated by spaces: ";
    std::cin >> name >> age;
    std::cout << "Hello " << name << "! You are " << age << " years old!";
```

You can also input **variables with whitespaces**. The problem is, it recognises it like 2 strings. To fix it, you can use this: 
``` C++
    std::cout << "Enter your full name: ";
    std::getline(std::cin,full_name);
    std::cout << "Hello " << full_name << "!" << std::endl;
```

### Output
There are 3 main ways to output (print) text: 
- `std::cout` - basic output message
- `std::cerr` - error output message
- `std::clog` - log output message

All of these output methods looks the same, but they might be useful in terminals, that supports different format of messages. This way you can see if it's just a normal message, log or error

## Execution model & Memory model

???

## Core language *vs.* Standard library *vs.* STL
- Core language
    - Most basics of C++ 
    - For example: 
        - `int number = 3;`
        - `int main(){}`
- Standard library
    - Set of ready to use, highly specialised components
    - For example:
        - `#include <iostream>`
        - `#include <string>`
- STL
    - ???
    - Highly specialised part of Standard library


***


## Variables and Data types

### Variables
Variable is named piece of memory, that stores specific type of data

Name of variable:
- Has to start with either a letter or an underscore (no with a number)
- Can contain letters, numbers and underscores (no spaces or special characters)
- Is case-sensitive (using of uppercase and lowercase letters matters)
&nbsp;  

Ways to init variables:
- Braced init
    - `int value{};`
    - if it's init'ed as empty, it's value will be 0
    - safer than functional init (you will get an error)
- Functional init
    - `int value(0);`
    - can't be empty
    - less safe than braced init (when float is given instead of, it will chop off the decimal part)
- Assignment init
    - `int value = 0;`
    - also chops off float to int

### Data types

| Syntax   | Example            | Description                  | Size |
|----------|--------------------|------------------------------|------|
| int      | `int a = 10;`      | whole number                 | 4 B  |
| double   | `double a = 10.1;` | decimal number (~ 6 digits)  | 8 B  |
| float    | `float a = 10.2;`  | decimal number (~ 15 digits) | 4 B  |
| char     | `char a = 'A';`    | single character             | 1 B  |
| bool     | `bool a = true;`   | true or false  (1 or 0)      | 1 B  |
| void     |                    |                              |      |
| auto     |                    | automatically deduced type   |      |

### Number systems in C++
There are 4 main number systems in C++:  

| Name        | Used symbols | Prefix     | Example                 |
|-------------|--------------|------------|-------------------------|
| Decimal     | 0 - 9        | \**none*\* | `int num = 15;`         |
| Octal       | 0 - 7        | 0          | `int num = 017;`        |
| Hexadecimal | 0 - 9; A - F | 0x         | `int num = 0x0f;`       |
| Binary      | 0, 1         | 0b         | `int num = 0b00001111;` |

All of these numbers equals the same, but in different number systems

#### Integer modifiers

| Name                       | Example                             |  From  |  To   | Size | Note                                 |
|----------------------------|-------------------------------------|:------:|:-----:|:----:|--------------------------------------|
| \**none*\*                 | `int value{10};`                    |  -2e9  |  2e9  | 4 B  |                                      | 
| Signed                     | `signed int value{10}`              |  -2e9  |  2e9  | 4 B  | Same as \**none*\*                   |
| Unsigned                   | `unsigned int value{-10}`           |   0    |  4e9  | 4 B  | Used to store positive numbers only  |
| Short                      | `short int value{10}`               | -32768 | 32768 | 2 B  | Uses less memory, but has less range |
| Long                       | `long int value{10}`                |        |       | 4 B  | Uses more memory, but has more range |
| Long Long                  | `long long int value{10}`           |        |       | 8 B  | Even bigger than long                |
| \*modifiers can be mixed\* | `unsigned long long int value{10}`  |

#### Fractional numbers
Basically umbers with decimal part. There are 3 types: 

| Name        | Example                     | Size | Precision   | Suffix     | Note                 |
|-------------|-----------------------------|------|-------------|------------|----------------------|
| Float       | `float num{1.2345f};`       | 4 B  | 7           | `f`        |                      |
| Double      | `double num{1.2345};`       | 8 B  | 15          | \**none*\* | Default, recommended |
| Long double | `long double num{1.2345L};` | 8+ B | > double    | `L`        |                      |

Precision = numbers after decimal point  
For example, the number 1.234567 has the precision of 7  
**You have to use the suffix**, otherwise they all will be doubles  
You can change the precision:  

``` C++
#include <iostream>
#include <iomanip>

using namespace std;

int main(){

    float num1{1.2345678901234567890123456789f};
    double num2{1.2345678901234567890123456789};
    long double num3{1.2345678901234567890123456789L};
    
    cout << setprecision(30);

    cout << num1 << endl;
    cout << num2 << endl;
    cout << num3 << endl;

    return 0;
}
```

### nan & inf
x/0 = inf  
0/0 = nan  

### Booleans
Data type, that represents either true or false value  
By default `true = 1` and `false = 0`  
You can change it with `cout << boolalpha;`, as you can see bellow

``` C++
#include <iostream>

using namespace std;

bool value {true};

int main(){

    cout << value << endl;
    cout << boolalpha;
    cout << value << endl;

    return 0;
}
```

### Characters
Characters (or chars) are variables, which represents a signle character.  
Characters can be assignes with either single quoter or ASCII value:
``` C++
char value1 = 'A';
char value2 = 65;
```
To find ASCII value, you can either use [ASCII table](https://theasciicode.com.ar/) or this:
``` C++
cout << static_cast<int>(value) << endl;
```

### Auto
Makes compiler automatically decide the type of variable.

| Example            | Type          |
|--------------------|---------------|
| `auto var{10}`;    | int           |
| `auto var{12.3};`  | double        |
| `auto var{12.3f};` | float         |
| `auto var{12.3l};` | double long   |
| `auto var{'e'};`   | char          |
| `auto var{123u};`  | unsigned      |
| `auto var{123ul};` | unsigned long |
| `auto var{123ll};` | long long     |

## Operations on data

**Basic operations**
| Name      | Sing |
|-----------|:----:|
| Add       | +    |
| Subtract  | -    |
| Multiple  | *    |
| Divide    | /    |
| Modulus\* | %    |

**Modulus** finds the remainder when one number is divided by another. Examples:  
`7 % 4 = 3` - 7 / 4 = 1, **3** remains  
`9 % 2 = 1` - 9 / 2 = 4, **1** remains  
`14 % 5 = 4` - 14 / 5 = 2, **4** remains

## Prefix and Postfix + and - 
`++` or `--` before or after int
Both increasing and decreasing works the same

### Prefix
Increase value before using it
``` C++
int value {5};
cout << ++value << endl;  // gives us 6
```

### Postfix 
Increase value after using it
``` C++
int value {5};
cout << value++ << endl;  // gives us 5
cout << value << endl;  // gives us 6
```

You can also use prefix/postfix like this:
``` C++
int value {5};
++value;
```

## Compound operators
These are used to simplify program... Let's say, you want to increase x by 5  
Instead of `x = x + 5`  
You can use `x += 5`  

| Available characters |
|----------------------|
| +                    | 
| -                    |
| *                    |
| /                    |

## Relational operators
Comparing operators **>**, **<**, **>=**, **<=** 
``` C++
int value1 {10};
int value2 {20};
cout << (value1 < value2) << endl;  // returns 1 (true)
cout << (value2 < value1) << endl;  // returns 0 (false)
```

## Logical operators
`&&` Returns true if a *and* b are true  
`||` Returns true if a *or* b are true  
`!` Returns *opposite value* of a  

|   a   |   b   | a && b |
|:-----:|:-----:|:------:|
| true  | true  |  true  |
| true  | false | false  |
| false | true  | false  |
| false | false | false  |

|   a   |   b   | a \|\| b |
|:-----:|:-----:|:--------:|
| true  | true  |   true   |
| true  | false |   true   |
| false | true  |   true   |
| false | false |  false   |

|   a   |  !a   | 
|:-----:|:-----:|
| true  | false |
| false | true  | 

[Continue tutorial](https://www.youtube.com/watch?v=8jLOx1hD3_o&t=16687s)
