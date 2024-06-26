# C++ Tutorial
My way of learning C++  
...once again...  

Tutorial i'm learning from: [C++ for Java Programmers by Mary Elaine Califf](https://www.youtube.com/watch?v=ZzaPdXTrSb8&)  
I already *\*cough\** know *\*cough\** Java, so this tutorial will (mostly) show the differences of C++ compared to Java

# Hello World
```c++  
#include <iostream>
// using namespace std;

int main() {
    std::cout << "Hello world!" << std::endl;
    return 0;
}
```

# Input/Output  
Standard input stream - **cin**  
Standard output stream - **cout**

```c++
std::cout << "Enter your age: ";

int age;
std::cin >> age;
std::cout << "Your age is: " << age << std::endl;

return 0;
```

# Primitive types
| Modifier | Minimum Size |
|-|-|
| short | 16 bits |
| long | 32 bits |
| long long | 64 bits |

| Integer Sign | Min            | Max           |
| ------------ | -------------- | ------------- |
| Signed       | -2_147_483_648 | 2_147_483_647 |
| Unsigned     | 0              | 4_294_967_295 |

0 is ***false***  
Everything other is ***true***

Keyword for constant is **const** rather than final  
Value has to be assigned to constant when declared, it cannot be changed afterwards  

# Functions
Functions can exist outside classes  

Order matters - you have to declare the function before using it  
By typing `#include <iostream>` you are putting all functions of *iostream* to your program  

### Example
#### Error
We tried to run *calculate()* before it was declared  
```c++
#include <iostream>

int main() {
    int result = calculate(5);
    std::cout << result << std::endl;
}

double calculate(double number) {
    return number * 2;
}
```

#### Fix #1
We moved *calculate()* before *main()*
```c++
#include <iostream>

double calculate(double number) {
    return number * 2;
}

int main() {
    int result = calculate(5);
    std::cout << result << std::endl;
}
```

#### Fix #2 - function prototype
It is **recommended** to use this way
```c++
#include <iostream>

double calculate(double number);

int main() {
    int result = calculate(5);
    std::cout << result << std::endl;
}

double calculate(double number) {
    return number * 2;
}
```

# Parameters 
## Types
### Pass by value
```c++
void func(int param){...}
```  
Default way, such as in Java  
We pass parameter to function, it gets converted to local variable and changes **won't be reflected** to the original variable  

### Pass by reference
```c++
void func(int& param){...}
```  
Any changes made to the parameters **will get reflected** to the original variable  

Pass by reference usually uses less memory *(?)*  

#### Const
If you don't want the variable to be modified, you can include *const* before the parameter, which makes it constant  
```c++
void func(const int& param){...}
```  

## Default arguments
```c++
void func(int minAge = 18){...}
```  
If you don't provide value when calling *func()*, it will make it 18 by default  
Default argument(s) has to be the last of all arguments (all the way on the right side)  
You can specify the default value just once, either in prototype *(preferred)* or in normal function declaration  

# Arrays
To declare, you specify type of objects in array, name of it and size  
You don't type **new**  
```c++
type name[size];
```  

Size of the array has to be a **constant**   
You have to specify the size of array (or it's elements), and it cannot be changed  
```c++
int score[10];
double price[NUM_ITEMS];

char vowels[] = {'a', 'e', 'i', 'o', 'u'};
int values[10] = {1, 2, 3, 4}  // other numbers will be zero
```  


**C++ has no way to check the size of array**  
To loop through array, you have to provide a number of elements  
You can actually access elements out of bounds of the array, it will give you another value from memory  

## 2D and multi-dimensional arrays 
```c++
int matrix[3][4];  // 2D array
int cube[3][3][3];  // 3D array
int something[1][2][3][4][5][6][7][8][9];  // 9D array, if you ever need it
```

## Arrays as Parameters
You can (don't have to) specify the size of array
```c++
void processArray(int nuberOfItems, int arr[])
void process3D(int numberPerRow, int arr[][10][10])
```

# Strings
## C-strings
Taken from C language  
Avoid when possible  

Array of characters, last character is null  
You must leave a space for null character  
```c++
char name[6] = "Peter";
```
`=` works only in declaration  
`==` doesn't work
`< > <= >= !=` doesn't work

### Functions
You need to `#include <cstring>` or include one of following: 

| Operation      | Library                                  |
| -------------- | ---------------------------------------- |
| Copy           | \<strncpy>                               |
| Concatenation  | \<strncat>                               |
| Comparison     | \<strncmp>                               |
| Finding length | \<strnlen>                               |
| Searching      | \<strchr>  <br>\<strrchr>  <br>\<strstr> |
Find more on [cplusplus.com](https://cplusplus.com/reference/cstring/)

### \<cctype>
Useful library for checking and manipulating strings

| Function             |
| -------------------- |
| int isalnum(int ch)  |
| int isalpha(int ch)  |
| int isblank(int ch)  |
| int iscntrl(int ch)  |
| int isdigit(int ch)  |
| int isgraph(int ch)  |
| int islower(int ch)  |
| int isprint(int ch)  |
| int ispunct(int ch)  |
| int isspace(int ch)  |
| int isupper(int ch)  |
| int isxdigit(int ch) |
| int tolower(int ch)  |
| int toupper(int ch)  |

## String class 
From C++ library 
Less problems than C-strings  

`#include <string>`

`=` works  
`==` works
`[]` works

```c++
string name = "Ann";

if (name == "Ann"){...}
if (name[0] <= 'M'){...}
major = preferredMajor;

cout << name.length() << endl;
cout << name.size() << endl;
```

You can read whole input line like this:
```c++
// only one word input 
cout << "enter a word: ";
cin >> word;

// whole line input
cout << "enter a phrase: ";
getline(cin, phrase);
```

## File Parameters
Here is how to read file parameters/arguments when 
```c++
#include <iostream>

int main(int argc, char* argv[]) {
	for (int i = 0; i < argc; i++)
	{
		std::cout << argv[i] << std::endl;
	}

	return 0;
}
```

# Pointers
Value of pointer is memory address  
```c++
int *i;
char *str;
Student *studentPointer;

int *p, *q
```

#### Address Operator `&`
Tells you address of pointer
```c++
int i, *ptr;
ptr = &i;
```

```c++
#include <iostream>

int main() {
	int i = 10;
	int *ptr = &i;
	  
	std::cout << i << std::endl;    // 10
	std::cout << ptr << std::endl;  // 0x7fff836c7c0c
	
	return 0;
}
```

```c++
std::cout << i << std::endl;    // 10
std::cout << ptr << std::enld;  // 0x7fff836c7c0c
std::cout << *ptr << std::endl; // 10
```

```c++
int i = 10;
int *ptr = &i;

std::cout << i << std::endl;     // 10
std::cout << ptr << std::endl;   // 0x7ffd7b964e8c
std::cout << *ptr << std::endl;  // 10

*ptr = 5;
std::cout << i << std::endl;     // 5
std::cout << ptr << std::endl;   // 0x7ffd7b964e8c
std::cout << *ptr << std::endl;  // 5
```

```c++
std::cout << ptr << std::endl;   // 0x7ffc0f9e8e0c - value of ptr
std::cout << *ptr << std::endl;  // 5 - dereferencing ptr = value of i
std::cout << &ptr << std::endl;  // 0x7ffc0f9e8e10 - 'pointer of pointer' = where is 'ptr' stored in memory
```

## Arrays and pointers
Array is just a pointer to the first value  
```c++
#include <iostream>

int main() {
	int myArray[10];
	int *myPointer = myArray;
	
	std::cout << myPointer << std::endl;   // 0x7ffc6194bf0
	std::cout << &myArray[0] << std::endl; // 0x7ffc6194bf0
	
	return 0;
}
```

And other values of array are just next places in memory
```c++
std::cout << &myArray[0] << std::endl; // 0x7ffc6194bf00
std::cout << &myArray[1] << std::endl; // 0x7ffc6194bf04
std::cout << &myArray[2] << std::endl; // 0x7ffc6194bf08
```

### Pointer Arithmetic
```c++
arr[i] == *(arr + i)
```
Therefore...
```c++
arr[0] == *arr
arr[1] == *(arr + 1)
arr[2] == *(arr + 2)
...
```
