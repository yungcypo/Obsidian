# Tmux
[Tmux](https://github.com/tmux/tmux/wiki) is a terminal thingy which let's you keep your sessions, manage windows and whatsoever :)

# Install
You will need to install `tmux` package with your package manager  

The next thing you will need it something called *Tmux Plugin Manager*, which is installed via Git  
```shell
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

Edit the configuration, located at **`~/.tmux.conf`**  
```shell
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

run '~/.tmux/plugins/tpm/tpm'`
```

Now it should be installed  
Run it simply with `tmux` command  

# Basic terms
Tmux consists of 3 main objects:
- Sessions
	- The main, topmost layer of Tmux
	- You can have any number of Sessions open up, but typically only attach to one
	- It contains one or more Windows, one of which is active
- Windows
	- Windows are inside Sessions
	- Similar to tabs in web browser
	- Only one can be active *(marked with `*`)*
	- Consists of one or more Panes
	- Info about Windows is show at the bottom of the screen
- Panes

You have Session, which can be split into Windows, which can be split into Panes  

# Commands/shortcuts/keybinds
Before entering any command, you have to press the `<prefix>` key, which is set to `ctrl + b` by default  

| Shortcut (Window) | Action                                 |
| ----------------- | -------------------------------------- |
| `c`               | Create new Window and set is as active |
| `<window_number>` | Set `<window_number>` as active Window |
| `n`               | Next Window                            |
| `p`               | Previous Window                        |
| `&`               | Kill window                            |
|                   |                                        |
|                   |                                        |

| Shortcut (Pane) | Action                                                                     |
| --------------- | -------------------------------------------------------------------------- |
| `%`             | Split to Panes vertically                                                  |
| `"`             | Split to Panes horizontally                                                |
| `←` `→` `↑` `↓` | Change active Pane                                                         |
| `{` `}`         | Move Pane                                                                  |
| `q`             | Toggle Pane number (Enter the number while toggled to switch to that Pane) |
| `z`             | Toggle zoom Pane to fullscreen                                             |
| `!`             | Make current Pane into window                                              |
| `x`             | Close pane                                                                 |


> Note: As said before, you have to hit `<prefix>` before any of these commands... I just didn't wrote it here because it'll be too long

# Sessions