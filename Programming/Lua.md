# Lua
[Lua](https://www.lua.org/about.html) is a powerful, efficient, lightweight, embeddable scripting language  
The reason I'm learning it is Neovim and it's configuration NvChad  

I will be learning from ["Learn basic Lua" by NvChad](https://nvchad.com/docs/quickstart/learn-lua/)  

# Hello World
Much like Python, it's starting good  
```lua
print("Hello World!")  
```

# Comments
```lua
-- single-line comment
```

```lua
--[[
	multi
	line
	comment
]]
```

# Variables & Data types
```lua
local n = 10  -- number
local name = "Peter"  -- string
local isAlive = true  -- booelan
local x = nil  -- no value / invalid  
```

Increment in numbers  
```lua
local n = 1
n = n + 1
print(n)

-- the += operator does not work
```

Concatenate strings  
```lua
local phrase = "My name is "
local name = "Peter"

print(phrase .. " " .. name)
print("My name is " .. "Peter")
```

# Comparison operator  
Almost the same as other languages  

| Operator | Meaning               |
| -------- | --------------------- |
| `==`     | Equal                 |
| `<`      | Less than             |
| `>`      | Greater than          |
| `<=`     | Less than or Equal    |
| `>=`     | Greater than or Equal |
| `~=`     | Not equal             |

# Conditional statements  
## `if`
```lua
local age = 21

if age > 18 then
	print("Over 18")
end
```

## `else` and `elseif`
```lua
local age = 21

if age > 18 then
  print("over 18")
elseif age == 18 then
  print("18 huh")
else
  print("kiddo")
end
```

## Boolean comparison
```lua
local isAlive = true
```

```lua
if isAlive then
	print("good to hear that")
end
```

Invert value with `not`
```lua
if not isAlive then
	print("oh no")
end
```

## String comparison
```lua
local name = "Peter"

if name ~= "Peter" then
	print("You are note Peter")
end
```

## Combining statements
```lua
if name == "Peter" and password == 12345678 then
	print("Access granted")
elseif name ~= "Peter" or password ~= 12345678 then
	print("Only one was right")
end
```

> Focus on `and` and `or`

# Functions 
```lua
local function print_num(a)
  print(a)
end

print_num(9)
```

```lua
local print_num = function(a)
  print(a)
end

print_num(9)
```

Multiple parameters  
```lua
function sum(a, b)
  return a + b
end
```

# Scope
```lua
function foo()
	local n = 10
end

print(n)  -- nil - it's because n is not accessible outside the function foo()
```

# Loops
## While loop
```lua
local i = 1

while i < 10 do
	print(i)
	i = i + 1
end
```

## For loop
```lua
for i = 1, 5 do
   print("hi")
end
```

# Tables
Tables are used to store complex data  
There are two types of tables: Arrays and Dictionaries

## Arrays
```lua
local colors = { "red", "green", "blue" }

print(colors[1])  -- first element
print(#colors)  -- size of table 
```

### Looping though Array Table  
```lua
for i = 1, #colors do
	print(colors[i])
end
```

#### `ipairs()`
You can loop though Table with `ipairs()`, which basically allows you to use `index` and `value` while looping though Table  
```lua
for index, value in ipairs(colors) do
	print(index)
	print(value)
end
```

## Dictionaries
```lua
local user = {
	name = "peter",
	age = 21,
	isAlive = true
}
```

Accessing Dictionary values  
Both lines will print the same  
```lua
print(user.name)
print(user["name"])
```

### Looping through Dictionary Table - `pairs()`
Similarly to [`ipairs()`](#`ipairs()`) is Arrays, you can use `pairs()` with dictionaries  
```lua
for key, value in pairs(user) do
	print(key .. ": " .. tostring(value))
end
```

## Nested Tables
Nested Array  
```lua
local matrix = {
	{1, 2, 3},
	{4, 5, 6},
	{7, 8, 9}
}

print(matrix[1][1])

for i = 1, #matrix do
	for j = 1, #matrix[i] do
		print(matrix[i][j])
	end
end
```

Nested Dictionary
```lua
local users = {
	peter = {age = 21, isAlive = true},
	jonatan = {age = 999, isAlive = false}
}
```

# Modules
Modules are meant to import code from other files  

```lua
require("abc")
require "abc"
-- both lines provide the same result
```

For example in `~/.config/nvim/lua`, all dirs and files are accessable via require  

Do note that all files in that lua folder are in path!  
`~/.config/nvim/lua/abc.lua`   
`~/.config/nvim/lua/abc/init.lua`  

# vim.tbl_deep_extend
This is a Neovim function which is used for merging tables and their values recursively  
Most plugins use it for merging config tables  
			
```lua
-- table 1
local person = {
    name = "joe",
    age = 19,
    skills = {"python", "html"},
}

-- table 2
local someone = {
    name = "siduck",
    skills = {"js", "lua"},
}

-- "force" will overwrite equal values from the someone table over the person table
local result = vim.tbl_deep_extend("force", person, someone)

-- result : 
{
    name = "siduck",
    age = 19,
    skills = {"js", "lua"},
}

-- The list tables wont merge cuz they dont have keys 
```
