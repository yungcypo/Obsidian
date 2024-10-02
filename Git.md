# First things first
## Check if git is already present
`git --version`

## Installing git
`sudo apt install git`

## Configure git
If you want to use [GitHub](https://github.com), use your username and email from there
`git config --global user.name "cyprich"`
`git config --global user.email "cypooriginal@gmail.com`

# Basic Commands
## git init
Makes git available for current directory

## git status
Shows the state of your project

## git log
Shows history of project  
### git log --graph --decorate --abbrev-commit --all --pretty=oneline

## git diff
Shows the difference in changed files

## git add \<file>
Adds file to git  
Makes file *staged*
### git add \*.png
Adds all png files
### git add .
Adds all files

## git restore --staged \<file>
Removes added files

## git commit
Makes commit  
### git commit -m "message"
Specifies commit message, so you don't have to deal with vim
### git commit -a
Commits all changed files, you don't have to *git add*  
Works only with changed files, if you create new file, you have to *git add*

## git checkout \<hash>
Goes back to commit marked with \<hash>
### git checkout master
Goes back to actual (newest) version
### git checkout -- \<file>
Removes changes in \<file>

## git clone \<URL> \<local_directory>
Clones repository from GitHub to your machine
> Note: this may cause problems because. See [[#Generate SSH key]] or follow [this tutorial](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) to fix problems  

## git push
Pushes commit to the server  
### git push origin master
Pushes to master branch
### git push -u origin master
Sets default value to *origin master*. Git will always push to *origin master*, unless you tell it to not  
You don't have to use *origin master* anymore

## git pull
Pulls commit from the server 
### git pull origin master
> Note: you may be asked, if you want to Merge or Rebase. For example, if you want to use Merge, type `git config pull.rebase false`

## git remote update
Checks for changes on remote server. Now when you hit `git status`, you will see that you need to pull

## git whatchanged
### git whatchanged origin/master -n 1
Similar to example before, provides more information, without `git status`

# Branches
## git branch
Shows all branches of repo
### git branch -vv
Shows all branches of repo with additional info
### git branch \<name>
Makes **new branch** with given \<name>
### git branch -d \<name>
Remove branch with given \<name>
## git checkout \<name>
		'Switches' to \<name> branch
### git checkout -b \<name>
'Switches' to \<name> branch, creates it, if not present
## git merge \<name>
Moves changes from \<name> to current branch   
For example, if I hit `git checkout master` and then `git merge new-feature`, I just got the *new-feature* to *master*

## Merge vs. Rebase

| Merge                      | Rebase                                      |
| -------------------------- | ------------------------------------------- |
| Non-destructive            | Destructive                                 |
| You are keeping 2 branches | You are keeping only 1 branch               |
| Parallel branches          | Takes one branch and sticks it to the other |

# Code from GitHub
Create a new repository on the command line
```
git init
git add README.md
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/cyprich/MinecraftServer.git
git push -u origin master
```

Push existing repository from the command line
```
git remote add origin https://github.com/cyprich/MinecraftServer.git
git branch -M master
git push -u origin master
```

## Moving `main` to `master`
```
git branch -m main master
git fetch origin
git branch -u origin/master master
git remote set-head origin -a
```

# Generate SSH Key
To avoid typing your password or token every time you push to a Git repository, you can set up an SSH key
1. Generate new SSH Key 
	- `ssh-keygen -t rsa -b 4096 -C cypooriginal@gmail.com`
2. Add the Key to GitHub account
	- Copy public key *(usually located at `~/.ssh/id_rsa.pub`)*
	- On [GitHub](https://github.com) go to *Account Settings > SSH and GPG keys*
	- Click *New SSH key* and paste here the public key
3. Change git remote URL from *HTTPS* to *SSH*
	- `git remote set-url origin git@github.com:cyprich/repo.git`


# Change remote URL
I changed my GitHub username, so I had to do this for every repo  
`git remote set-url origin git@github.com:cyprich/Obsidian.git`  