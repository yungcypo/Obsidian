# ZSH
Configuration of ZSH  

`echo $SHELL` - view your current shell

# Installing and Enabling ZSH
## Install 
`sudo apt install zsh` - Debian-based OS
`sudo pacman -S zsh` - Arch-based OS 

## Change default shell 
`chsh cyprich` and enter your password  
Enter location of ZSH, usually `/bin/zsh` *(make sure it's there before proceeding)*  

**Make sure you have git installed** by typing `git --version`  
Backup existing ZSH config by `mv ~/.zshrc ~/.zshrc.bak`  

# Configure ZSH
Make new config `nano ~/.zshrc`  
All following commands will be written to this file  

## Plugin manager - Zinit

| Command                                                                                                                                                               | Description                                          |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| `ZINIT_HOME="${XDG_DATA_HOME:-${HOME}/.local/share}/zinit/zinit.git"`<br>                                                                                             | Set the directory we want to store Zinit and plugins |
| `if [ ! -d "$ZINIT_HOME" ]; then` <br>`    mkdir -p "$(dirname $ZINIT_HOME)"`<br>`    git clone https://github.com/zdharma-continuum/zinit.git "$ZINIT_HOME"`<br>`fi` | Download Zinit, if it's not there yet                |
| `source "${ZINIT_HOME}/zinit.zsh"`                                                                                                                                    | Source/Load Zinit                                    |
Now open new terminal  
You should see git cloning something the first time you log in  
To make sure everything is working type `zinit zstatus`  

## Nerd Font
If you are going to use custom prompt (section after this one), you need to use some Nerd Font    
Nerd Font is like a normal font, but it's packed with bunch of icons which are useful in things like this  
My favorite is [JetBrainsMono Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/JetBrainsMono.zip), but you can choose any of [available Nerd Fonts](https://www.nerdfonts.com/)  

### Installation
- Using command `wget <link>`, download your desired font    
- Unzip downloaded file and move it to `~/.fonts`  
- Run command `fc-cache -fv`  

> Note: You might need to install `unzip` and `fontconfig` 

## Prompt
Prompt is like the visual way of seeing in your console  
There are two big guys there: `Powerlevel10k` and `oh-my-posh`  
You can choose one of them, or keep the default one  

### oh-my-posh
Install `oh-my-posh` with following command  

| Command                                              | Description          |
| ---------------------------------------------------- | -------------------- |
| `curl -s https://ohmyposh.dev/install.sh \| bash -s` | Install `oh-my-posh` |

Add following to `~/.zshrc`

| Command                         | Description      |
| ------------------------------- | ---------------- |
| `eval "$(oh-my-posh init zsh)"` | Add `oh-my-posh` |
#### Fixing path
You might see error like `oh-my-posh: command not found`  
This might happen because the install folder of `oh-my-posh` is `~/.local/bin` by default  
Add following to `~/.zshrc` BEFORE any command related with `oh-my-posh`  
`export PATH=$PATH:/home/username/.local/bin`  

> Note: Change `username` with you actual username 
> Note: If you don't know your username, type the command `whoami`

#### Configuring themes
You can download one of [available themes](https://ohmyposh.dev/docs/themes) and add following to configuration to use it   
``eval "$(oh-my-posh init zsh --config path/to/downloaded/file)"``, so it looks something like this   

| Command                                                              | Description                   |
| -------------------------------------------------------------------- | ----------------------------- |
| `eval "$(oh-my-posh init zsh --config ~/Downloads/atomic.omp.json)"` | Add custom `oh-my-posh` theme |

To see changes, you have to re-open your terminal  
If you have problems, check [Oh My Posh website](https://ohmyposh.dev/)


### Powerlevel10k

Add following to `~/.zshrc`

| Command                                                | Description       |
| ------------------------------------------------------ | ----------------- |
| `zinit ice depth=1; zinit light romkatv/powerlevel10k` | Add Powerlevel10k |
Open up a new terminal and follow steps to configure *Powerlevel10k*  
To reconfigure p10k, type `p10k configure`   

## Plugins

| Command                                         | Description         |
| ----------------------------------------------- | ------------------- |
| `zinit light zsh-users/zsh-syntax-highlighting` | Syntax highlighting |
| `zinit light zsh-users/zsh-autocompletion`      | Autocompletion      |

## Settings
### History settings

| Command                       |
| ----------------------------- |
| `HISTSIZE=5000`               |
| `HISTFILE=~/.zsh_history`     |
| `SAVEHIST=$HISTSIZE`          |
| `HISTDUP=erase`               |
| `setopt appendhistory`        |
| `setopt sharehistory`         |
| `setopt hist_ignore_space`    |
| `setopt hist_ignore_all_dups` |
| `setopt hist_save_no_dups`    |
| `setopt hist_ignore_dups`     |
| `setopt hist_find_no_dups`    |

### Keybinds

| Command                                                                                 |
| --------------------------------------------------------------------------------------- |
| *!!! not complete command* `bindkey` `history-search-backward` `history-search-forward` |
| `bindkey -e`                                                                            |
| ```bindkey '^[[1;5C' emacs-forward-word```                                              |
| ```bindkey '^[[1;5D' emacs-backward-word```                                             |
| `bindkey '^H' backward-kill-word`                                                       |
> Note: To show keystrokes, run command `showkey -a`

### Aliases

| Command                   |
| ------------------------- |
| `alias ls='ls -l --color` |

### Disable underline

| Command                                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ```(( ${+ZSH_HIGHLIGHT_STYLES} )) \|\| typeset -A ZSH_HIGHLIGHT_STYLES```<br>`ZSH_HIGHLIGHT_STYLES[path]=none`<br>`ZSH_HIGHLIGHT_STYLES[path_prefix]=none` |

# Config file
There is the whole configuration file in this folder, it's called `.zshrc.p10k` or `.zshrc.ohmyposh`, depending on the prompt of your choice  
Simply take this file and place it in your home directory, and rename it to `.zshrc`  
You can simply do it with command `mv .zshrc.ohmyposh ~/.zshrc` (if you are currently in the same folder as this file)  