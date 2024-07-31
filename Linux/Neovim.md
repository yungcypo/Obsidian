# Neovim
[Neovim](https://neovim.io/) is a highly extensible, keyboard-based and very powerful text editor  

# `:Tutor`
Typing this command, you will get 30-minute tutorial, if you are new to Vim  

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
> Here ends the 3rd episode of `:Tutor` and I will leave it like so for a while and continue later