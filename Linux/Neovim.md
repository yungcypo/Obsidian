# Neovim
[Neovim](https://neovim.io/) is a highly extensible, keyboard-based and very powerful text editor  

# `:Tutor`
Typing this command, you will get 30-minute tutorial, if you are new to Vim  

> I don't know why it it called a "30-minute tutorial", when it took me like 2 days, but whatever

# Moving cursor

| Key | Shortcut          |
| --- | ----------------- |
| k   | Move cursor up    |
| j   | Move cursor down  |
| l   | Move cursor right |
| h   | Move cursor down  |
```
     ↑
     k
← h     l →
     j
     ↓
```

**Hint**
The h key is at the left and moves left
The l key is at the right and moves right
The j key looks like down arrow

To **move the cursor to the start of the line**, press `0`  
To **move the cursor to the end of the line**, press `$`  

# Exiting Neovim
1. Press the `<Esc>` key to enter Normal mode
2. Type `:q` to exit Neovim
	 - If you type `:wq` you will save changes and exit (write, quit)
	 - If you type `:q!` you will exit without saving changes

Pressing `<Esc>` will place you in Normal mode or cancel any partially completed command

# Text editing
## Deletion
Press `x` to delete the character under the cursor  
Press `dw` to delete to the end of a word  
Press `d$` to delete to the end of a line  
Press `dd` to delete whole line

You basically just type `d` with following [motion](#Motions) (discussed later)
## Insertion
Press `i` to insert text  
## Addition
Press `A` to append text  
This will basically move cursor at the end of a line and enter insert mode  

# Editing a file  
To open a file in Neovim, type `nvim <filename>` in the console  
For example `nvim helloworld.py`  

# Operators and Motions
Many commands that change text are made from an operator and a motion  
Command can look like this: `<operator><motion>`, for example `dw` *(delete word)*
For example, the delete command:   
- Operator is `d`
- Motions could be
	- `w` - until the start of the next word, EXCLUDING its first character 
	- `e` - to the end of current word, INCLUDING the last character
	- `$` - to the end of current line, INCLUDING the last character  

## Operators and Motions with Numbers
Typing a number with and operator repeats it that many times  
Command can look like this: `<operator><number><motion>`
For example:
- `d3w` *(delete 3 words)*
- `2dd` *(delete 2 lines)* *(special case)*

## Motions

| Motion      | Meaning                                          |
| ----------- | ------------------------------------------------ |
| `0`         | **Start** of current **line**                    |
| `$`         | **End** of current **line**                      |
| `b`         | **Start** of current **word**                    |
| `w`         | **End** of current **word** (with whitespace)    |
| `e`         | **End** of current **word** (without whitespace) |
| `gg`        | **Start** of the **file**                        |
| `G`         | **End** of the **file**                          |
| `<number>G` | **Line** with given **number**                   |


# Undo
Press `u` to undo the last command  
Press `U` to undo a whole line  
Press `<ctrl> + <r>` to *"undo the undos"*, so basically a **Redo**

# Put
Type `p` to put previously deleted text after the cursor  
Type `P` to put previously deleted text before the cursor  

# Replace
Type `rx` to replace the character at the cursor with `x`  
So basically, you type `r` and then the letter you want to replace with  

# Change 
Change operator
Type `ce` to change until the end of a word  
It basically deletes whole word after cursor and enters Insert mode

For example, if you have the word `baloon` and you want to change it to `banana`  
1. You put your cursor on the letter `a`
2. You press `ce` 
3. You type `nana`
4. You press `<Esc>` to exit Insert mode

Change operator uses the same motions as the Delete operator, the format is `c [number] <motion>`   
This means that `w` *(word)* and `$` *(end of line)*  

| Replace             | Change                                    |
| ------------------- | ----------------------------------------- |
| `r`                 | `c`                                       |
| Not an operator     | Operator                                  |
| Replaces one letter | Changes one or more *(depends on motion)* |
| Normal mode         | Insert mode                               |

# Search
Type `/` followed by phrase to search for the phrase  
After pressing `<enter>`, you can switch between occurrences  

Press `n` to go to the next occurrence  
Press `N` to go to the previous occurrence  

To search for a phrase in the backward direction, use `?` instead of `/`   
This will search the last occurrence first   

To go back to older positions, press `<ctrl> + o`
To go forward to newer positions, press `<ctrl> + i`

To turn off highlights after search, type the command `:noh`  

## Find matching parenthesis  
If you want to find a pair to any kind of parenthesis (`(`, `[`, `{`) , just put cursor on it and press `%`  
With `%` you can switch between opening and closing parenthesis

# Substitute
Type `:s/old/new` to substitute (change) `new` for `old`  
This will substitute only the first occurrence of `old` into `new`  
To substitute all occurrences, type `:s/old/new/g`  

To substitute every occurrence of a phrase between two lines, type `:#,#s/old/new/g` where `#`'s is the line range you want to change in  
For example `:1,5s/old/new/g` will substitute all occurrences of `old` with `new` between lines `1` and `5`  

To substitute all occurrences in **whole file**, type the command `:%s/old/new/g`  

To substitute all occurrences in **whole file, with confirmation**, type the command `:%s/old/new/gc`  
You will be asked before every occurrence if you want to replace it  

# External command
To execute external command, type `:!` followed by `<command>`  
With this you are able to execute any command, as if you were out of Neovim  
For example, type `:!ls` to list the contents of a directory  
Remember to press `<enter>` to run the command  

# Writing to file
You already know that typing `:wq` will *write* to the file and *quit* Neovim  
What wasn't mentioned yet is that typing `:w` followed by `<filename>` allows you to save to different file  

If you want to write just a part of a file, you can do so with **visual mode**  
1. Move the cursor to the first line of text you want to save 
2. Press `v` to enter visual mode
3. Move the cursor to the last line of text you want to save. Notice that text will get selected   
4. Press `:` (You will see `:'<,'>` at the bottom of your screen)  
5. Type `w FILENAME` to write selected text to file named `FILENAME`

# Retrieving   
If you have a file, that you want to copy to file currently open in Neovim, type `:r FILENAME` where `FILENAME` is the name of the file  
After doing so, you can see the content of the file placed under your cursor  

If you want to retrieve from external command, type `:r` followed by `!<command>`  
For example, typing `:r !ls` will list the contents of your directory and place it under you cursor  

> Note: Don't mistake `:r` (retrieving) with `r` (removing)

# Open
Type `o` to *open* new line **below** you cursor  
If you have a cursor on a line, and you will type `o`, it will create new line under your cursor, move you there and enter insert mode  

To create a new line **above**, type `O` (capital `o`)

# Append
Press `a` to enter insert mode after the cursor  

This is very similar to [pressing `i`](#Insertion), which enters the insert mode before the cursor  
The only difference is where the characters are inserted  

# Replace 2
We already covered [replace](#Replace)  
You pressed `rx` to *replace* the letter under cursor with `x`  

If you press `R`, you will enter Replace mode where you are able to replace more than one letter  
Press `<esc>` to exit Replace mode

# Copy
Use the `y` operator to copy text  
`y` stands for yank

Use `p` to paste text after cursor (either copied or deleted)  
Use `P` to paste text before cursor  

# Moving between windows
To move between windows (if you have more than one), you need to press `<ctrl> w <ctrl> w`  
Another window will open (for example) if you press `F1` for help  