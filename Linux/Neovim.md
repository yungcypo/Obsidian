# Neovim
[Neovim](https://neovim.io/) is a highly extensible, keyboard-based and very powerful text editor  
Neovim is a fork of [Vim](https://www.vim.org/)  
If you don't know how Vim works, check [Vim tutorial](./Vim.md) first, to avoid any inconveniences and confusion  

Now, I will focus on the configurations on Neovim and stuff like that  
I will be following ["Neovim for Newbs" tutorial by "typecraft" on YouTube](https://www.youtube.com/watch?v=zHTeCSVAFNY&list=PLsz00TDipIffreIaUNk64KxTIkQaGguqn)  

# First steps
Before starting, make sure to:  
- Know how to use Vim
- Have Neovim installed
	- You can do so with your package manager, like `sudo pacman -S neovim` or `sudo apt install neovim`

# `init.lua`
`init.lua` is a configuration file for Neovim  
Make new file in `~/.config/nvim/init.lua`  
If you already have this file, make sure to make a backup if you don't want to lose it  

We can type the following...

```lua
vim.cmd("set tabstop=4")
vim.cmd("set softtabstop=4")
vim.cmd("set shiftwidth=4")
```

...to set width of `<tab>` to 4 characters  

To apply changes, type the command `:source %`  
Make sure your new file is saved   

## Package manager - `lazy.nvim`
[`lazy.nvim`](https://github.com/folke/lazy.nvim) is one of two most popular package managers for Neovim  

> The other one is [`packer.nvim`](https://github.com/wbthomason/packer.nvim), but I will stick to `lazy` in this tutorial  

### Installation 
Go to [their website](https://lazy.folke.io/installation) and copy given script to corresponding files  

> Note: I chose "Single File Setup"

```lua
-- Bootstrap lazy.nvim
-- Bootstrap lazy.nvim
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not (vim.uv or vim.loop).fs_stat(lazypath) then
  local lazyrepo = "https://github.com/folke/lazy.nvim.git"
  local out = vim.fn.system({ "git", "clone", "--filter=blob:none", "--branch=stable", lazyrepo, lazypath })
  if vim.v.shell_error ~= 0 then
    vim.api.nvim_echo({
      { "Failed to clone lazy.nvim:\n", "ErrorMsg" },
      { out, "WarningMsg" },
      { "\nPress any key to exit..." },
    }, true, {})
    vim.fn.getchar()
    os.exit(1)
  end
end
vim.opt.rtp:prepend(lazypath)

-- Make sure to setup `mapleader` and `maplocalleader` before
-- loading lazy.nvim so that mappings are correct.
-- This is also a good place to setup other settings (vim.opt)
vim.g.mapleader = " "
vim.g.maplocalleader = "\\"

-- Setup lazy.nvim
require("lazy").setup({
  spec = {
    -- add your plugins here
  },
  -- Configure any other settings here. See the documentation for more details.
  -- colorscheme that will be used when installing plugins.
  install = { colorscheme = { "habamax" } },
  -- automatically check for plugin updates
  checker = { enabled = true },
})
```

Now if you type the command `:Lazy`, a GUI of Lazy will pop up   

## Color scheme  
I will be using the [Catppuccin](https://github.com/catppuccin/nvim) color scheme  
Go to the link, and copy Installation script from there  
Paste it into `init.lua`, under where it says `-- add your plugins here`

```lua
-- add your plugins here
{ "catppuccin/nvim", name = "catppuccin", priority = 1000 }
```

Also, you need to tell Catppuccin to set up, and set the color scheme in Neovim

```lua
require("catppuccin").setup()
vim.cmd.colorscheme "catppuccin"
```

If you close and re-open Neovim, you should see the new color scheme installing and being used right after  

## Telescope
[`telescope.nvim`](https://github.com/nvim-telescope/telescope.nvim) is a tool for fuzzy finding files, `grep` through files and more  
Go to the link, look for `lazy.nvim` section and paste given code to `init.lua`

```lua
-- add your plugins here 
{
    'nvim-telescope/telescope.nvim', tag = '0.1.8',
    dependencies = { 'nvim-lua/plenary.nvim' }
}
```

> Don't forget to add comma between `catppuccin` and `telescope` plugins  

Also add following code to the end of a file, to actually use `telescope`  

```lua
local builtin = require("telescope.builtin")
vim.keymap.set('n', '<C-p>' builtin.find_files, {})
```

Now after restarting Neovim, you can hit `<ctrl> p` to find files  

I will also set "Live grep" to `<ctrl> l` like this  

```lua
vim.keymap.set('n', '<C-l>' builtin.live_grep, {})
```

## Treesitter
[Treesitter](https://github.com/nvim-treesitter/nvim-treesitter) is a package used for highlighting and indenting  

Add this to the list of plugins  

```lua
-- add your plugins here
{"nvim-treesitter/nvim-treesitter", build = ":TSUpdate"}
```

I got it from [Wiki - Install - `lazy.nvim`](https://github.com/nvim-treesitter/nvim-treesitter/wiki/Installation) on their Github, it''s a part of the code here  

To load configs, add this to the end of `init.lua`

```lua
local config = require("nvim-treesitter.configs")
config.setup({
	ensure_installed = { "lua", "javascript", "html", "python" },
	highlight = { enable = true },
	indent = { enable = true },
})
```

