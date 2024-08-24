# C++ tutorial
## Hello World
``` C++
#include <iostream>

int main(){
    std::cout << "Hello World!" << std::endl;
    return 0;
}
```
`#include <iostream>` - import library so you can use terminal  
`int main(){}` - main function in C++  
`std::cout` - function to print something to terminal  
`std::endl;` - newline character - puts next text on new line  
`return 0` - tells the program that everything is correct  
\**Almost* every line has to end with semicolon - `;` 


***
## Drawing a shape
``` C++
#include <iostream>
using namespace std;

int main(){
    // Drawing simple shape
    cout << "    /|" << endl;
    cout << "   / |" << endl;
    cout << "  /  |" << endl;
    cout << " /   |" << endl;
    cout << "/____|" << endl;

    return 0;
}
```
\*`using namespace std;` so you don't have to type `std::` every time

***
## Variables
``` C++
#include <iostream>
using namespace std;
int main(){

    string characterName = "John";
    int characterAge = 35;

    cout << "There once was a mane named " << characterName << endl;
    cout << "He was " << characterAge << " years old" << endl;
    cout << "He liked the name " << characterName << endl;
    cout << "But did not like being " << characterAge << endl;

    return 0
}
```


***
## Data types

| Syntax   | Description                  | Size |
|----------|------------------------------|------|
| string   | text                         |      |
| int      | whole number                 | 4 B  |
| double   | decimal number (~ 6 digits)  | 8 B  |
| float    | decimal number (~ 15 digits) | 4 B  |
| char     | single character             | 1 B  |
| bool     | true or false  (1 or 0)      | 1 B  |
| auto     | automatically deduced type   |      |
| void     |                              |      |


***
## Working with Strings
``` C++
string phrase = "Giraffe Academy";
```
`phrase.length();` - length of string = 15  
`phrase[0];` - letter with index 0 of phrase = G  
\*Counting starts at 0 = 1st is 0; 2nd is 1 and so on  
`phrase[0] = B;` - changes 1st letter to B = Biraffe Academy  
`phrase.find("Academy");` - returns an index, where does given word starts
`phrase.find("Academy", x)` - x is optional argument **(int)**. It tells the program, at what index to start looking  
`phrase.substr(x, y)` - substring - gives us part of a string; starting at x **(int)**, y **(int)** characters long



***
## Working with numbers

``` C++
#include <iostream>
using namespace std;

int main(){

    cout << 40 << endl;  // 40
    cout << -40.0249464 << endl;  // -40.0249
    cout << 10 + 2 << endl;  // 12
    cout << 20 - 5 << endl;  // 15
    cout << 10 * 5 - 6 << endl;  // 44
    cout << (4 + 5) / 11 * 5 - 3 << endl;  // -3
    cout << 10 % 3 << endl;  // 1

    return 0;
}
```
\* Everything that starts with `//` is a comment

### cmath library
``` C++
#include <iostream>
#include <cmath>
using namespace std;

int main(){

    cout << pow(2, 8) << endl;  // 2^8 = 256
    cout << sqrt(81) << endl; // Square root of 81 = 9
    cout << round(5.3) << endl; // Round 5.1 = 5
    cout << ceil(5.3) << endl; // Rounds to bigger int = 6
    cout << floor(5.3) << endl; // Rounds to smaller int = 5
    cout << fmax(3, 10) << endl; // Returns biggest number = 10
    cout << fmin(3, 10) << endl; // Returns smallest number = 3

    return 0;
}
```


## Getting User Input
``` C++
#include <iostream>
using namespace std;

int main(){

    double age;
    cout << "Enter your age: ";
    cin >> age;  // Getting user input and storing it as age variable

    cout << "You are " << age << " years old!" << endl;

    return 0;
}
```
Notice that you have to use `>>` instead of `<<`  
This method has 1 problem - you are not able to put space here. If you wanted to get user's name, and he puts a space here, only the first word is going to be recognised  
To fix it, you can use function `getline()`  
``` C++
#include <iostream>
using namespace std;

int main(){

    string name;
    cout << "Enter your name: ";
    getline(cin, name);  // gets input and storing it as name variable
    cout << "Hello " << name << "!";

    return 0;
}
```


***
## Simple Calculator
``` C++
#include <iostream>
using namespace std;

int main(){

    int num1, num2;
    
    cout << "Enter first number: ";
    cin >> num1;
    cout << "Enter second number: ";
    cin >> num2;

    cout << "Your answer is: " << num1 + num2 << endl;

    return 0;
}
```


***
## Arrays
``` C++
int luckyNumbers[] = {4, 8, 15, 16, 23, 42};
cout << luckyNumbers[0];  // 4
luckyNumbers[0] = 7  // changes 1st int to 7

int unluckyNumbers[20] = {5, 10, 40}  // you can put 20 ints here
```



***
## Functions 
``` C++
#include <iostream>
using namespace std;

void sayHi (){
    cout << "Hello User!";
}

int main(){

    sayHi()

    return 0;
}
```
\*Void is most basic type of function, which is not gonna return a function  
You can also do it like this, to make it more... better
``` C++
#include <iostream>
using namespace std;

void sayHi (string name, int age){
    cout << "Hello " << name << "!" << endl;
    cout << "You are " << age << " years old!" << endl << endl;
}

int main(){

    sayHi("Peter", 18);
    sayHi("JozkoFerko", 9);
    sayHi("Mia", 2);

    return 0;
}
```


*** 
## Return Statement
``` C++
double cube(double num){
    return num * num * num
}
cout << cube(10) << endl; // 1000
```


***
## If Else Statements
``` C++
#include <iostream>
using namespace std;


int main(){

    bool isMale = true;

    if (isMale){
        cout << "You are a male" << endl;
    } else {
        cout << "You are not a male" << endl;
    }
    
    cout << endl;

    bool isDay = true;
    bool isRaining = false;

    if (isDay){
        if(!isRaining){
            cout << "Go outside" << endl;
        } else {
            cout << "Don't go outside, it's raining" << endl;
        }
    } else {
        cout << "It's night, go sleep" << endl;
    }

    return 0;
}
```


***
## Better Calculator
``` C++
#include <iostream>
using namespace std;

double calc(double num1, char sign, double num2){
    if (sign == '+'){
        return num1 + num2;
    } else if (sign == '-'){
        return num1 - num2;
    } else if (sign == '*'){
        return num1 * num2;
    } else if (sign == '/'){
        return num1 / num2;
    } else {
        return 0;
    }
}

int main(){

    double num1, num2;
    char sign;

    cout << "Enter first number: ";
    cin >> num1;
    cout << "Enter operator sign: ";
    cin >> sign;
    cout << "Enter second number: ";
    cin >> num2;

    cout << endl << calc(num1, sign, num2);

    return 0;
}
```


***
## Switch Statements
Switch statement is basically a special type of if statement, which allows us to check one particular value against a bunch of other values  
``` C++
#include <iostream>
using namespace std;

string getDayOfWeek(int dayNum){
    string dayName;

    switch (dayNum){
        case 1:
            dayName = "Monday";
            break;
        case 2:
            dayName = "Tuesday";
            break;
        case 3:
            dayName = "Wednesday";
            break;
        case 4:
            dayName = "Thursday";
            break;
        case 5:
            dayName = "Friday";
            break;
        case 6:
            dayName = "Saturday";
            break;
        case 7:
            dayName = "Sunday";
            break;
        default:
            dayName = "Invalid Day Number";
    }

    return dayName;
}

int main(){

    int dayNum;

    cout << "Enter a day number: ";
    cin >> dayNum;

    cout << getDayOfWeek(dayNum) << endl;

    return 0;
}
```


***
## While Loops
``` C++
int index = 1;
while(index <= 5){
    cout << index << endl;
    index++;
}
```

### Do While Loops
'Inverse while loops' - first it executes the code, then checks for the condition
``` C++
int index = 6;
do {
    cout << index << endl;
    index++;
} while(index <= 5);
``` 


***
## For Loops
``` C++
for (int i = 0; i < 5; i++){
    cout << i << endl;
}
```
`for (statement 1; statement 2; statement 3){}`  
**Statement 1** is executed (one time) before the execution of the code block  
**Statement 2** defines the condition for executing the code block  
**Statement 3** is executed (every time) after the code block has been executed  
&nbsp;  
`for (initialization; condition; update){}`  
**Initialisation** - initializes variables, is executed only once  
**Condition** - if *true*, the body of the loop is executed, if *false*, the loop is terminated  
**Update** - updated the value of initialized variables and again checks the condition  
&nbsp;  

### Range Based For Loop
``` C++
int num_array[] = {1, 3, 5, 2, 8, 4, 1, 8};
for (int n : num_array) {
    cout << n << endl;
}
```
\**This one's better imo*


## Exponent Function
``` C++
#include <iostream>
using namespace std;

int main(){

    double num;
    int exp;
    double result = 1;

    cout << "Enter number: ";
    cin >> num;
    cout << "Enter exponent: ";
    cin >> exp;

    for (int i = 1; i <= exp; i++){
        result *= num;
    }

    cout << result << endl;

    return 0;
}
```


***
## 2D Arrays & Nested For Loops
``` C++
int numberGrid[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

for (int i = 0; i < 3; i++){
    for (int j = 0; j < 3; j++){
        cout << numberGrid[i][j] << endl;
    }
}
```



***
## Pointers
Pointer is a type of information. It stores the value of where is a variable located in RAM. 
`cout << &name;` to get memory adress of the variable *name*  
Memory adress can look like this: `0xdda05ff5f0` *for example*  

``` C++
#include <iostream>
using namespace std;

int main(){

    int age = 19;
    int *pAge = &age;

    double gpa = 1.7;
    double *pGpa = &gpa;

    string name = "Peter";
    string *pName = &name;

    // To get memory adress
    cout << pAge << endl;
    cout << pGpa << endl;
    cout << pName << endl;

    // To get data from memory adress = dereferencing
    cout << *pAge << endl;
    cout << *pGpa << endl;
    cout << *pName << endl;

    cout << *&gpa; // getting a memory adrees and then value from it

    return 0;
}
```


***
## Classes & Objects
``` C++
#include <iostream>
using namespace std;

class Book {
    public:
        string title;
        string author;
        int pages;
};


int main(){

    Book book1;
    book1.title = "Harry Potter";
    book1.author = "JK Rowling";
    book1.pages = 500;

    cout << book1.title;

    return 0;
}
```


## Constructor Functions
``` C++
#include <iostream>
using namespace std;

class Book {
    public:
        string title;
        string author;
        int pages;

        Book(){
            title = "no title";
            author = "no author";
            pages = 0;
        }

        Book(string aTitle, string aAuthor, int aPages){
            title = aTitle;
            author = aAuthor;
            pages = aPages;
        }
};


int main(){

    Book book1("Harry Potter", "JK Rowling", 500);
    Book book2("Lord of the Rings", "Tolkien", 700);

    return 0;
}
```

## Object Functions
``` C++
class Student {
    public:
        string name;
        string major;
        double gpa;

        Student(string aName, string aMajor, double aGpa){
            name = aName;
            major = aMajor;
            gpa = aGpa;
        }

        bool hasHonors(){
            if (gpa >= 3.5){
                return true;
            } else {
                return false;
            }
        }

};
```
``` C++
#include <iostream>
using namespace std;

class Student {
    public:
        string name;
        string major;
        double gpa;

        Student(string aName, string aMajor, double aGpa){
            name = aName;
            major = aMajor;
            gpa = aGpa;
        }

        bool hasHonors(){
            if (gpa >= 3.5){
                return true;
            } else {
                return false;
            }
        }

};


int main(){

    Student student1 ("Jim", "Business", 2.4);
    Student student2 ("Pam", "Art", 3.6);

    return 0;
}
```

## Getters and setters

``` C++
#include <iostream>
using namespace std;

class Movie {
    private:  // available only inside class
        string rating;
    public:  // available everywhere
        string title;
        string director;
        Movie(string aTitle, string aDirector, string aRating){
            title = aTitle;
            director = aDirector;
            setRating(aRating);
        }

        void setRating(string aRating){
            if (aRating == "G" || aRating == "PG" || aRating == "PG-13" || aRating == "R"){
                rating = aRating;
            } else {
                rating = "NR";
            }
        }

        string getRating(){
            return rating;
        }
};


int main(){

    Movie avengers("The Avengers", "Joss Whendon", "PG-13");
    
    cout << avengers.getRating() << endl;

    avengers.setRating("Dog");  // enters invalid rating
    cout << avengers.getRating() << endl;

    return 0;
}
```


## Inheritance
``` C++
#include <iostream>
using namespace std;

class Chef {  // superclass
    public: 
        void makeChicken(){
            cout << "The chef makes chicken" << endl;
        }
        void makeSalad(){
            cout << "The chef makes salad" << endl;
        }
        void makeSpecialDish(){
            cout << "The chef makes BBQ ribs" << endl;
        }    
};

class ItalianChef : public Chef{  // subclass
    public:
        void makePasta(){
            cout << "The chef makes pasta" << endl;
        }
        void makeSpecialDish(){
            cout << "The chef makes chicken parm" << endl;
        }
};


int main(){

    Chef chef;
    chef.makeChicken();

    ItalianChef italianChef;
    italianChef.makePasta();

    cout << endl;

    chef.makeSpecialDish();
    italianChef.makeSpecialDish();


    return 0;
}
```

***  
***  

## Dynamic Arrays - Vector
Similar to array or list, but the **size is dynamic**  
`std::vector<datatype> name;`
``` C++
#include <iostream>
#include <vector>
using namespace std;

int main(){

    vector<int> items = {10, 11, 12, 13};
    items.push_back(100);

    // normal for loop to print values
    for(int i = 1; i < items.size(); i++){
        cout << items[i] << endl;
    }

    //range-based for loop to print values
    for(int n:items){
        cout << n << endl;
    }

    return 0;
}

```

### Sorting Vector
``` C++
#include <iostream>
#include <vector>
#include <bits/stdc++.h>
using namespace std;

int main(){
    vector <int> v1 {1, 5, 8, 9, 6, 7, 3, 4, 2, 0};
    // sort in ascending order
    sort(v1.begin(), v1.end());

    vector <int> v2 {1, 5, 8, 9, 6, 7, 3, 4, 2, 0};
    // sort in descending order
    sort(v2.begin(), v2.end(), greater<int>());


    for(int i:v1){
        cout << i << " ";
    }

    cout << endl;

    for(int i:v2){
        cout << i << " ";
    }

    return 0;

}
```


***
## Pairs
Pair is used to combine together two values that may be of different data types  
`pair <datatype1, datatype2> pairName;`
``` C++
#include <iostream>
using namespace std;

int main(){
    
    pair <int, char> myPair1;
    myPair1.first = 100;
    myPair1.second = 'A';

    pair <int, char> myPair2(200, 'B');

    cout << myPair1.first << " " << myPair1.second << endl;
    cout << myPair2.first << " " << myPair2.second << endl;

    return 0;

}
```
## Lowercase, Uppercase
Return only lowercase letters
``` C++
string str = "bEEFGBuFBRrHgUHlNFYaYr";
string result;
for(int i = 0; i < str.lenght(); i++)
    if(islower(str[i])){
        result += str[i];
    }
cout << result << endl;
```




















