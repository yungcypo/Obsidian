# Python
[Python](https://www.python.org/) is a high-level general-purpose programming language  
This is the first language that I learned, so don't expect much from this :)  

# Hello World
```python
print("Hello World!")
```

```python
print("   /|")
print("  / |")
print(" /  |")
print("/___|")
```

# Variables
Imagine you have a story about character named *John*   
You will write a whole book about *John*  
But later on, you will decide that you don't like the name *John* and you want to change it to *Mike*  

We can use a **variable** to define the name  
We can use the variable instead of the name  
When we will want to change the name, we can change the variable and everything will change  

```python
character_name = "John"
character_age = "35"
print("There once was a man named " + character_name + ", ")
print("he was " + character_age + " years old.")
print("He really liked the name" + character_name + ", ")
print("but didn't like being " + character_age + ".")
```

Now, we will re-write the whole story only with changing the value of variable   

```python
character_name = "Tom"
character_age = "50"
print("There once was a man named " + character_name + ", ")
print("he was " + character_age + " years old.")
print("He really liked the name" + character_name + ", ")
print("but didn't like being " + character_age + ".")
```

You can also change the variable mid-program, like this

```python
character_name = "John"
character_age = "35"
print("There once was a man named " + character_name + ", ")
print("he was " + character_age + " years old.") 

character_name = "Mike"
print("He really liked the name" + character_name + ", ")
print("but didn't like being " + character_age + ".")
```

# Comments
Comment in Python (and other programming languages) is something that you can write, and it will be ignored by program   
It's main purpose is to leave a note for you or another programmer, that is looking at your code  
In Python, you can make a comment with `#`, like this

```python
print("Hello there, how are you")  # this is an comment
```

If Python sees a `#` in a line, it will ignore everything until the end of a line  
Comments does not change the way the code works  



# Data Types
There are different types of variables in Python  

## String
In example before, we stored `string` in the variable `character_name`, which is basically a text  

```python
name = "John"
```

## Number
You can also store a `number` in variable

```python
age = 21
```

> Note: Notice how `string` had quotes (`""`), whereas `number` does not
> In example before we had quotes around a number, just to make some things simpler... You will see [in a moment ](#Printing%20string%20and%20number%20together)  

## Float
`float` is a number with floating decimal point  
This basically means that it's a number with decimal part  

```python
my_float = 3.14
weight = 61.3
```

> Note: Notice how we have decimal dot `.` instead of decimal comma `,`  
> If we wanted to have decimal comma instead, we will got an error  
> Comma in Python is used to things like [lists](#Lists) which will be covered later in tutorial

## Boolean
There is also a `boolean` data type, which can be either `True` or `False`  

```python
is_john_male = True
is_john_female = False
```

> Note: The first letter or `True` or `False` has to be capital  


# Printing string and number together 
If you already tried to print a `string` along with a `number` in one print statement, you got an error  
In Python, you can't do this  
There is a way around it, which is to convert `number` to `string`, like this 

```python
print(str(my_number))
```

Like this you can convert the number into string, and you can *(obviously)* use it as string  

```python
name = "Peter"
age = 18

print("Hello " + name + " you are " + str(age) + " years old")
```

# Working with `string`
Let's print some string first...

```python
print("Giraffe Academy")
```

We can add a "new line" inside a string with adding `\n`, something like this  

```python
print("Giraffe\nAcademy")
```

Imagine we wanted to print quotes (`"`)   
We can't just put it there like so, because it will end the sentence we want to print  
But we can do so with `\"`  
The backslash (`\`) will make Python kind of ignore the quote (`"`), and it will treat it like a text instead of a special character 

```python
print("Giraffe\"Academy")
```

We can also print variable with string, as we seen before  

```python
phrase = "Giraffe Academy"

print(phrase)
print(phrase + "is cool")

```

> Note: Notice where I put quotes and where I did not
> If I wrote `print("phrase")`, the output will be `phrase` instead of `Giraffe Academy`

## String functions  
Function is a little block of code that will do a specific operation for us  
Functions on strings can be used to modify given string

Print string in lowercase or uppercase

```python
print(phrase.lower())  # giraffe academy
print(phrase.upper())  # GIRAFFE ACADEMY
```

Check, if phrase is already uppercase  
It will give us [Boolean](#Boolean) value whenever it is uppercase or not   
If we used the phrase from example above, it will give us `False`, because the whole phrase is not uppercase  

```python
print(phrase.isupper())  # False
```

What will you get with following code? 
If you said `True`, you are right   
First, the phrase gets "converted" to uppercase, then it checks if it's uppercase, which obviously is  

```python
print(phrase.upper().isupper())  # True
```

With this code you can the the number of letters in the phrase   
`len` stands for "length", so basically you are looking for the length of the phrase  

```python
print(len(phrase))  # 15
```

To get the first letter of phrase, you can do following   
Good thing to mention, **counting in programming usually starts with 0, not with 1**  
So if you want to get 1st character, you need to request the *0th* character 

```python
print(phrase[0])  # G
```

With this code, you can find the location (index) of given character  
If the phrase had multiple of given characters, it will return the location of first occurrence *(like in second line of code)*  

```python
print(phrase.index("G"))  # 0
print(phrase.index("a"))  # 3
```

We can also look for more that one character

```python
print(phrase.index("Acad"))  # 8
```

If we were looking for a character or text, that is not present in phrase, we will get an error 

```python
print(phrase.index("BOO"))  # *Error*
```

You can also replace a piece of string with another 

```python
print(phrase.replace("Giraffe", "Elephant"))  # Elephant Academy
```

There are a lot more String function than these, I will stop it there for simplifying reasons  

# Working with numbers
You can print numbers just like so  

```python
print(3)
print(3.141592)
print(-2.9)
```

You can also put a math expression inside the print statement, Python will evaluate it  

```python
print(4 + 3)  # 7
print(2 * 7)  # 14
print(15 / 3)
print(3 * (4 + 5)) # 27
```

A bit less know operator is modulus (`%`)  
It is the remainder after division  
If we had code like this... 

```python
print(10 % 3)
```

...it will do `10 / 3`, which is equal to `3` and `1` is left, so it will return `1`  

Take a look at some other examples  

```python
print(12 % 5)  # 2
print(17 % 4)  # 1
print(10 % 2)  # 0
print(7 % 10)  # 7
```

It's a normal math operation, it's just less known  

## Number functions
Similarly to [String funcitons](#String%20functions), also Numbers have functions  

```python
print(abs(10))  # absolute value of 10 = 10
print(abs(-10))  # absolute value of -10 = 10
print(pow(3, 2)) # 3 to the power of 2 = 3^2 = 9

print(max(1, 9)) # prints the biggest of given numbers = 9
print(min(1, 9)) # prints the smalles of given nubmers = 1

print(round(3.14))  # rounds the number = 3
```

There are some more modules in the *math library*  
You don't need to worry what that means right now, you just need to import it at the beginning of file  

```python
from math import *

print(floor(9.876))  # rounding to nearest smaller number = 9
print(ceil(1.234))  # rounding to nearest bigger number = 2

print(sqrt(36))  # square root = 6
```

# Getting input
Sometimes you want to get something from the user using your program  
You can do it with `input()` function, like this  

```python
name = input("Enter your name: ")
```

User will enter his name and it will be stored in `name` variable  

```python
name = input("Enter your name: ")
age = input("Enter your age: ")

print("Hello " + name + " you are " + str(age) + " years old")
```

You can also have empty `input()`, like the following code, but it may lead to confusion  

```python
name = input()
```

You don't even have to store it inside a variable  

```python
input()
```

# Basic calculator
A really basic calculator, which you can make with previous knowledge   

```python
num1 = input("Enter a number: ")
num2 = input("Enter another number: ")
result = num1 + num2
print(result)
```

# MadLibs Game
```python
color = input("Enter a color: ")
noun = input("Enter a noun: ")
plural_noun = input("Enter a plural noum: ")

print("Roses are " + color) 
print(plural_noun + " are blue")
print("I love " + noun)
```

# Lists
Lists in Python are basically a variables, which can store multiple values  
Lets make a list of friends for example  

```python
friends = ["Kevin", "Karen", "Jim"]
```

Notice how the list is defined with square brackets `[]` and individual values are separated with comma `,`

You can print this list with `print(list_name)`  
This will print the list the same way as it was declared  

```python
print(friends)  # ["Kevin", "Karen", "Jim"]
```

But sometimes we don't want to print the list like this  
Lets have a look how to access specific elements  

## Accessing list elements 
You can access a list element with `list_name[index_of_element]`   
As I mentioned before, **counting starts from 0** instead of 1  
That means that if we want to get first friend, we have to request a friend with the index of zero  

```python
print(friends[0])  # Kevin
```

To print the last friend, we can use this cool feature  

```python
print(friends[-1])  # Jim
```

If we wanted to access element that does not exist, we will get an error  

```python
print(friends[999])  # *Error*
```

Now lets say we have a larger list 

```python
friends = ["Kevin", "Karen", "Jim", "Oscar", "Toby", "Max", "Johny", "Ezhekiel"]
```

We want to print multiple elements, but not all of them   
We can use something called \____   

```python
print(friends[1:4])  # "Karen", "Jim", "Oscar"
```

Previous code will print elements from index 1 *(2nd element = Karen)* all the way to element with index 4, not including 4 (4th element = Oscar)

If I did the following, it will print all elements form the index of 1 to the end of this list  
We basically ignored the `end`, and by default it's set to the size of the list  

```python
print(friends[1:])  # "Karen", "Jim", "Oscar", "Toby", "Max", "Johny", "Ezhekiel"
```

If I ignored the first value, it will be set to `0` by default  

You can add second semicolon with a number after, which will define *step*  
By default, the step is one, which means it will print the whole list  
You can set the step to `2` to print every second element, or to `3` to print every third element  
You can also print the list in reverse order by setting the step to `-1`  

```python
print(friends[::2])  # every second = ['Kevin', 'Jim', 'Toby', 'Johny']
print(friends[::3])  # every third = ['Kevin', 'Oscar', Johny']
print(friends[::-1])  # reverse order = ['Ezhekiel', 'Johny', 'Max', 'Toby', 'Oscar', 'Jim', 'Karen', 'Kevin']
print(friends[::-2])  # in reverse order, every second = ['Ezhekiel', 'Max', 'Oscar', 'Karen']
```

Notice how I can ignore individual parts, and it will be set to the default value, resulting in printing the same list  

```python
print(friends[0:7:1])  # "Karen", "Jim", "Oscar", "Toby", "Max", "Johny", "Ezhekiel"
print(friends[0::1])  # "Karen", "Jim", "Oscar", "Toby", "Max", "Johny", "Ezhekiel"
print(friends[::1])  # "Karen", "Jim", "Oscar", "Toby", "Max", "Johny", "Ezhekiel"
print(friends[::])  # "Karen", "Jim", "Oscar", "Toby", "Max", "Johny", "Ezhekiel"
```

## Change a value in list 
Following code will replace the first value ("Karen") with "Peter"  
We can see this by printing the list  

```python
friends[0] = "Peter"  # "Peter", "Jim", "Oscar", "Toby", "Max", "Johny", "Ezhekiel"
```

## List functions  

### `list.append(value)`
With following function we can add another value to the end of a list  

```python
friends.append("Daniel")
print(friends)  # "Peter", "Jim", "Oscar", "Toby", "Max", "Johny", "Ezhekiel", "Daniel"
```

### `list.insert(index, value)`
If we  don't want to insert to the end of a list, but somewhere else, we can use `insert` function  
With following code,  we set `Alex` to be the element with the index of 2 *(third element)* and all the other will be pushed to the right  

```python
friends.insert(2, "Alex") # "Peter", "Jim", "Alex", "Oscar", "Toby", "Max", "Johny", "Ezhekiel", "Daniel"
```

### `list.pop()`  
`pop` is like an opposite function to `append`, it removes the last value   

```python
friends.pop()
print(friends) # "Peter", "Jim", "Alex", "Oscar", "Toby", "Max", "Johny", "Ezhekiel"
```

### `list.remove(value)`  
If we wanted to remove specific value from list, we can use `remove` function   

```python
friends.remove("Alex")
print(friends) # "Peter", "Jim", "Oscar", "Toby", "Max", "Johny", "Ezhekiel"
```

### `list.extend(another_list)`
If we had two lists and we will want to combine it to one, for whatever reason   

```python
lucky_numbers = [3, 7, 9]
numbers = [10, 11, 12]

numbers.extend(lucky_numbers)
print(numbers)  # [10, 11, 12, 3, 7, 9]
```

We had the `numbers` list, and we basically added the `lucky_numbers` list to the end of it 


### `list.index(element)`
Prints the index of given element in list 

```python
print(friends.index("Oscar"))  # 3
print(friends.index("askdfha"))  # *Error*, because this value is not in a list  
```


### `list.count(element)`
As the name suggests, `count` function will print the number of occurrences of element in list 

```python
my_list = [1, 1, 1, 3, 4, 6]
print(my_list.count(1))  # 3
print(my_list.count("1"))  # 0 - we have numbers, not strings 
print(my_list.count(6))  # 1
print(my_list.count(99)) # 0
```

### `list.sort()`
This will sort the list in alphabetical order  

```python
friends.sort()
print(friends)  # ['Ezhekiel', 'Jim', 'Johny', 'Karen', 'Kevin', 'Max', 'Oscar', 'Toby']
```

If the list consists of numbers, it will sort the numbers  

```python 
my_list = [6, 5, 4, 7, 4, 9, 1, 6, 7]

my_list.sort()
print(my_list)  # [1, 4, 4, 5, 6, 6, 7, 7, 9]
```

### `list.reverse()`
This will reverse the list  

```python
friends.reverse()
print(friends)  # ['Ezhekiel', 'Johny', 'Max', 'Toby', 'Oscar', 'Jim', 'Karen', 'Kevin']
```

### `new_list.copy(old_list)`  
This will copy `old_list` into `new_list`  
So basically you will have two of the same lists   

```python
new_friends = friends.copy()

print(friends)  # "Karen", "Jim", "Oscar", "Toby", "Max", "Johny", "Ezhekiel"
print(new_friends)  # "Karen", "Jim", "Oscar", "Toby", "Max", "Johny", "Ezhekiel"
```


# Tuples
A Tuple in Python is something similar to List, but with one major difference  
Tuple can't be changed  
Once you define a tuple, it's elements cannot change  

```python
my_tuple = (3.14, 9, 1.23456, "Hello")
```

Notice how tuple is defined with `()` whereas list was defined with `[]`  

## Accessing Tuple elements
This works the same as in [Lists](#Accessing%20list%20elements)  

```python
print(my_tuple[0])  # 3.14
```

The value of element or the number of elements cannot be changed   

# Advanced Lists and Tuples  
In Python, you can freely combine [Lists](#Lists) and [Tuples](#Tuples) together (and even [Dictionaries](#Dictionaries), which will be covered later)  
In chapters before, the *type of element* was either a Number, String, or Float  
We can totally put there a Boolean also, or even a List or Tuple as a value  

## 2D List
### Creating 2D List
Lets make a List  
But instead of Numbers, it will be storing a Lists  
```python
my_matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]  

# you can split it in multiple lines, to make it look more organized  
another_matrix = [
	[9, 8, 7],
	[6, 5, 4],
	[3, 2, 1]
]
```

Cool, right?  
We just created a "2D List"  
In fact, this is a List of Lists of Numbers  

### Accessing 2D List elements
Remember how we accessed elements in normal List?  
We just typed `list[index]` and we got a Number  
But now, instead of Numbers, we have Lists there  
So what we do? It's as simple as `list[index][index]`  
With first index, we received a List, so we  need to access it elements with another `[index]`

```python
print(my_matrix)  # [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(my_matrix[0])  # [1, 2, 3]
print(my_matrix[0][0])  # 1
```

## 3D List
We can also create 3D, 4D and so on...

```python
my_3d_list = [
	[
		[1, 2, 3], [4, 5, 6]
	],
	[
		[7, 8, 9], [0, 1, 2]
	],
	[
		[3, 4, 5], [6, 7, 8]
	]
]

print(my_3d_list)  # [[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [0, 1, 2]], [[3, 4, 5], [6, 7, 8]]]
print(my_3d_list[0])  # [[1, 2, 3], [4, 5, 6]]
print(my_3d_list[0][1])  # [4, 5, 6]
print(my_3d_list[0][1][2])  # 6
```

3D list is technically a List of Lists of Lists of Numbers  
You see that it can get pretty messy if I put everything in one line, that's why I prefer writing it to multiple lines, even if it's not required

## Combining structures
We can also put a Tuples inside of Lists or Lists inside of Tuples

```python
coordinates = [
	(3, 4), (6, 2), (80, 64)
]

points = (
	[2, 4, 6, 12],
	[7, 5, 6, 2],
	[4, 6, 0, 0]
)
```

Accessing elements from those should be pretty straight forward, we already did this  

```python
print(coordinates)  # [(3, 4), (6, 2), (80, 64)]
print(coordinates[0])  # (3, 4)
print(coordinates[0][1])  # 4

print(points)  # ([2, 4, 6, 12], [7, 5, 6, 2], [4, 6, 0, 0])
print(points[1])  # [7, 5, 6, 2]
print(points[1][3])  # 2
```

This way you can create any structure you need  
Just remember that Tuples cannot be changed, so once you have a Tuple, it's there forever  

# Functions
## Basic stuff about Functions
Lets say you have a piece of code, which you wanted to execute multiple times  

```python
my_list = []

my_list.append(1)
print(my_list)

my_list.append(1)
print(my_list)

my_list.append(1)
print(my_list)
```

Now the code gets pretty big   
And imagine if you wanted to execute like 300 lines of code multiple times   
...Now you changed your mind and you want to do something different   

Good solution for this is a *function*  
Let's define a function to see what I am talking about  
Use `def function_name():` to define a function  

```python
def do_something_with_list():
```

Now we kind of made a function, but we will get error because it's empty  
The code you want to put inside a function must be *indented* with `tab` key on your keyboard   

```python
def do_something_with_list():
	print("Running function...")
	my_list.append(1)
	print("Your list just got extended")
	print("I will print the list in the line bellow")
	print(my_list)
	print("Function done...")
```

When you run the code right now, it seems like nothing happened  
Why? Because, actually, nothing happened  
We never told the function to run - we did never **call the function**  
We need to call the function in order to run  
It's as easy as writing it's name along with parenthesis, like in example bellow  

```python
do_something_with_list()  
```

Now we called the function and you can see all the text we defined in the function  

We can call the function multiple times, you can see how the list expands  

```python
do_something_with_list() 
do_something_with_list() 
do_something_with_list() 
do_something_with_list() 
do_something_with_list() 
```

Now we saved a lot of work huh?  
It can be even shorter, you will see in a while  

## Function parameters  
In the previous function, we added `1` to the end of a list every time  
What if we wanted to add a different number every time  

We can add something called *parameter* to the function definition  
I'm pretty sure you noticed those parentheses in function definition  
The parameter name is written in between the parenthesis, like in example bellow  

```python
def do_something_with_list(number_to_add):
	...
```

Now we just created a kind of variable, that can be used only inside the function  
Now we can adjust the function, to add out desired number, not just `1`

```python
def do_something_with_list(number_to_add):
	print("Running function...")
	my_list.append(number_to_add)
	print("Your list just got extended with " + str(number_to_add) + ". The whole list now looks like this: ")
	print(my_list)
	print("Function done...")
```

When calling function with parameters, we *have to* write those parameters there  

```python
do_something_with_list(1) 
do_something_with_list(5) 
do_something_with_list(3) 
do_something_with_list(6) 
do_something_with_list(7) 
```

We can add as many parameters as we want  

```python
def say_hi(name, age):
	print("Hello " + name + ", you are " + str(age) + " years old")


say_hi("Peter", 21)  # Hello Peter, you are 21 years old
say_hi("Adka", 15)  # Hello Adka, you are 15 years old
say_hi("Jarko", 10)  # Hello Jarko, you are 10 years old
```

If we had some variable in our code, we can freely pass it to function as it's parameter  

```python
my_name = "Peter"
my_age = 21


def say_hi(name, age):
	print("Hello " + name + ", you are " + str(age) + " years old")


say_hi(my_name, my_age)
```

## Return statement  
Maybe sometimes in code, we don't want a function print anything  
We might want the function just to do something or calculate something, so we can use the value later on  

Let's say that we want to calculate the volume of a cube  
> Note: Remember that we *don't want to print* the value right now  

```python
def cube_volume(size):
	size * size * size


cube_volume(5)  # *This won't print anything*
print(cube_volume(5))  # None
```

This function takes one argument - size of a cube - and calculates it's volume  
Calling the function will seemingly do nothing  
In fact, the function did run, but we didn't told it what to do with the result  

We can tell it to **run the function, and give us the value** by using `return`  

```python
def cube_volume(size):
	return size * size * size


cube_volume(5)  # *This won't print anything once again*
print(cube_volume(5))  # 125
```

There you have it!  
The function ran, and *returned* 125  
You can imagine it like the `cube_volume(5)` is being replaced by 125, which is the `return` value  

We can use this more...  

```python
def cube_volume(size):
	return size * size * size


print("The cube with size of " + str(3) + " has a volume of " + str(cube_volume(3)))  # The cube...3...volume of 27
print("The cube with size of " + str(4) + " has a volume of " + str(cube_volume(4)))  # The cube...4...volume of 64
print("The cube with size of " + str(2 + 5) + " has a volume of " + str(cube_volume(2 + 5)))  # The cube...7...volume of 343

print("Both cubes together have the volume of " + str(cube_volume(3) + cube_volume(4)))  # ...volume of 91
print("If we subtracted the volumes, we will get " + str(cube_volume(4) - cube_volume(3)))  # ...we will get 37

```

As you might see, we can use even math operations as parameters  

You can also see the versatility of the function this way. If you put the `print` statement directly inside the function, you will always get the same result  
If you wanted to print something different, you will have to create a new function  

