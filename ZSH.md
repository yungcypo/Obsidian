# ZSH
Configuration of ZSH  

`echo $SHELL` - view your current shell

## Installing and Enabling ZSH
### Install 
`sudo apt install zsh` - Debian-based OS
`sudo pacman -S zsh` - Arch-based OS 

### Change default shell 
`chsh cyprich` and enter your password  
Enter location of ZSH, usually `/bin/zsh` *(make sure it's there before proceeding)*  

**Make sure you have git installed** by typing `git --version`  
Backup existing ZSH config by `mv ~/.zshrc ~/.zshrc.bak`  

## Configure ZSH
Make new config `nano ~/.zshrc`  
All following commands will be written to this file  

### Plugin manager - Zinit

| Command                                                                                                                                                              | Description                                          |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| `ZINIT_HOME="${XDG_DATA_HOME:-${HOME}/.local/share}/zinit/zinit.git"`<br>                                                                                            | Set the directory we want to store Zinit and plugins |
| `if [ ! -d "$ZINIT_HOME" ]; then` <br>`    mkdir -p "$(dirname $ZINIT_HOME)`<br>`    git clone https://github.com/zdharma-continuum/zinit.git "$ZINIT_HOME"`<br>`fi` | Download Zinit, if it's not there yet                |
| `source "${ZINIT_HOME}/zinit.zsh"`                                                                                                                                   | Source/Load Zinit                                    |
Now open new terminal  
You should see git cloning something the first time you log in  
To make sure everything is working type `zinit zstatus`  

### Prompt - Powerlevel10k
First, you need to install Nerd font, for example [JetBrainsMono Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/JetBrainsMono.zip) using command `wget <link>`  
Unzip downloaded file and move it to `~/.fonts`  
Run command `fc-cache -fv` 
> You might need to install `unzip` and `fontconfig` 

Add following to `~/.zshrc`

| Command                                                | Description       |
| ------------------------------------------------------ | ----------------- |
| `zinit ice depth=1; zinit light romkatv/powerlevel10k` | Add Powerlevel10k |
Open up a new terminal and follow steps to configure *Powerlevel10k*  
To reconfigure p10k, type `p10k configure`   

### Syntax highlighting

| Command                                         | Description                 |
| ----------------------------------------------- | --------------------------- |
| `zinit light zsh-users/zsh-syntax-highlighting` | Syntax highlighting plugins |

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

### Aliases

| Command                   |
| ------------------------- |
| `alias ls='ls -l --color` |
### Disable underline

| Command                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `(( ${+ZSH_HIGHLIGHT_STYLES} )) \|\| typeset -A ZSH_HIGHLIGHT-STYLES`<br>`ZSH_HIGHLIGHT_STYLES[path]=none`<br>`ZSH_HIGHLIGHT_STYLES[path_prefix]=none` |
