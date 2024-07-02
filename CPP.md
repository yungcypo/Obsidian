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
int values[10] = {1, 2, 3, 4};
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

# Dynamic Memory Management
Usage of pointers  

## `new` 
`new` keyword allocates space for a data in the heap  
Returns a pointer to that item  
Can be used for any type (not just classes)  

```c++
int* myPtr = new int;
string* myStringPtr = new string("hello");
```

## Dynamic Arrays
Dynamic Arrays get automatically initialized and allocated, unlike static arrays  
Dynamic Arrays are resizable  
```c++
string* names = new string[24];
int* score = new int[10]{4, 5, 10, 12};
```

```c++
// Dynamic array
int* score = new int[10];
for (int i = 0; i < 10; i++)
{
	std::cout << score[i] << " ";
}
// Output: 4 10 21 7 0 0 0 0 0 0

std::cout << std::endl;

// Static array
int score2[10];
for (int i = 0; i < 10; i++)
{
	std::cout << score2[i] << " ";
}
// Output: 1651076199 779647075 1600677166 1819242352 -1205882080 32766 -970284800 32524 -968353456 32524 %
```

#### Managing Dynamic Arrays
Things you need to store:
- Pointer to the first element
- Capacity of the array
- If the array is not full, you need the number of items

#### Growing Dynamic Array
```c++
if (itemsInArray == capacity) {
	capacity *= 2;
	int* temp = new int[capacity];
	
	for (int i = 0; i < itemsInArray; i++) {
		temp[i] = originalArray[i];
	}
	delete [] originalArray;
	originalArray = temp;
}
```

## Cleaning up
Unlike Java, C++ doesn't have Garbage Collector, so we have to manually free the memory  
We don't need to worry about statically-allocated variables, only dynamic needs to be freed  

For dynamically-allocated variables, we need to use `delete`   
```c++
delete myPtr;
delete [] myArray;
```

`delete` doesn't change the value of pointer  
`delete` doesn't change the value of the target of pointer  
`delete` only **tells the system, that the memory is no longer in use**, so that it **can be re-allocated**

## Memory leak
Imagine we have code like this: 
```c++
int *ptr = new int;
*ptr = 5;
ptr = new int;
*ptr = 10;
```

What happens here?  
1. Allocate space for new int
2. Set the value to 5
3. Allocate *another* space for new int
4. Set the value to 10

Now we have **no way to access** the value 5, this is called **memory leak**  
Program will allocate more and more memory, making it slower and eventually crashing  

## Dangling Pointers
Pointers to memory, that has already been freed  
Pointer that points to deleted memory  
Using **delete** to Dangling Pointer will generally **crash the program**  

```c++
int *ptr;
ptr = new int;

delete ptr;
delete ptr; // we got error here
```

If we had 2 pointers, pointing to the same address, we will get error as well
```c++
int *ptr1, *ptr2;
ptr1 = new int;
ptr2 = ptr1;

std::cout << ptr1 << std::endl << ptr2 << std::endl;  // we can see the same address here

delete ptr1;
delete ptr2; // we got error here
```

# Classes
Bit more complex than in Java  
It is split into two parts
- Class declaration
	- Typically in `.h` file
	- Function prototypes 
	- Ends with semicolon (`;`)
- Class implementation
	- Typically in `.cpp` file
	- This is where the function is really written
	- Method name is preceded by `className::` 
		- `::` is scope operator in C++, instead of `.` in Java
		- `Enemy.name` in Java is the same as `Enemy::name` in C++
If the method is simple (one line), you can write it directly at declaration in `.h` file  

By default, things are **private**  

## Classes terminology
Comparison with Java  

| Java             | C++              |
| ---------------- | ---------------- |
| *parts of class* | Members          |
| Instances        | Data members     |
| Methods          | Member functions |

## Class example
*date.h*
```c++
#include <string>

class Date {
	private:
		int day;
		int month;
		int year;
	
	public: 
		Date();
		// Date(): Date(1, 1, 1970) {}  // using the second constructor
		Date(int theDay, int theMonth, int theYear): day(theDay), month(theMonth), year(theYear) {}
		
		int getDay() const {return day;}
		std::string getShortDate() const;
		int getMonth() const {return month;}
		
		void setDay(int day) {this->day = day;}
};
```
**`.h` file ends with `;` !!!**

*date.cpp*
```c++
#include "date.h"

Date::Date() {
	day = 1;
	month = 1;
	year = 1970;
}

std::string Date::getShortDate() const {
	return std::to_string(day) + ". " + std::to_string(month) + ". " + std::to_string(year);
}
```

*daterunner.cpp*
```c++
#include <iostream>
#include "date.h"

int main() {
	// Static objects
	Date defaultDate;
	Date schoolStart(1, 9, 2024);
	
	std::cout << defaultDate.getShortDate() << std::endl;
	std::cout << schoolStart.getShortDate() << std::endl;
	defaultDate.setDay(31);
	std::cout << defaultDate.getShortDate() << std::endl;
	
	// Dynamic objects
	Date* birthday = new Date(4, 6, 2003);
	std::cout << birthday->getShortDate() << std::endl;
	birthday->setDay(13);
	std::cout << birthday->getShortDate() << std::endl;
	
	return 0;
}
```

- `Date defaultDate`
	- Actually declaring the date (statically)
	- If we did `Date defaultDate()`, C++ will think, that we are making function returning Date
- `Date scholStart(1, 9, 2024)`
	- Calling the other constructor with parameters/arguments
- `defaultDate.getShortDate()`
	- Calling `getShortDate()` method from `Date` class
- `Date* birthday = new Date(4, 6, 2003)`
	- Declaring the date dynamically
	- We have to use `->` instead of `.`

## Compiling multiple files
`g++ date.cpp daterunner.cpp`  
`g++ date.cpp daterunner.cpp -o daterunner`

## `const` on Methods
`std::string getName() const {return name;}`  
Making returned value constant, making it **unable to change**  
Basically **every getter** should have `const`  

## Inline functions
Similar to macros *(?)* but safer  
More efficient on short functions  
Less efficient on long functions

## `->`
*"just like `.` but for pointers"*  

When I reference part of an object that I have a pointer to, I use this **arrow operator**
`somePointer->getMajor();`  

The dot operator (`.`) has higher precedence that the dereference operator, so `*somePointer.getMajor();` produces an error  
We can use it like this: `(*somePointer).getMajor();`  


