					                                    Git Commands Cheat sheet
Git is a version control system or source code management tool
It is where code and related files are stored
It is used to Track the changes in files
it will maintain multiple versions of same file
Git hub is used to do collabrative work and Projects.
It is centralized source and shraing repository.
its is a platform independent
it is free and open-source
They can handle larger projects efficiently
They can save time and developers can fetch and create pull request without switching.

Working directory:It is a stage where git is only aware of having project files in that working folder
		        It will not track these files until we commit those files

Staging area: The staging area is like rough draft space, Its where you can add the version of a file or multiple files that you want to save in the next commit. In other words, the next version of your project.
Repository: Repository in the git is considered as your project folder
	        A repository contains the all the project related data
	        It contains the collection of the files and also history of changes made of those files

Types of repository: 
                1.Local Repository: The local repository is everything in your .git directory.Mainly what you will see in you local repository are all of your checkpoints or commits. It is a area that saves everything (so do not delete the repository)

	     2.Central Repository: It will be present in the Git hub where u can share all of your files. You need to add and commit your files before you push into github.

	     3.Remote Repository: It will be present on remote host where you can share all your files to remote machines.

Git-Hub:
    • Git hub is a web-based platform used for version control
    • It simplifies the process of working with other people and makes it easy to collaborate on projects 
    • team members can work on files and easily merge their changes in with the master branch of the project.

Now if you want to Push your code to git hub

    • Git remote add origin (Url name of git hub repository)
    • git push -u origin (branch-name)
Go to git hub and check the files you pushed


##### Setting up git
$ git config --global user.name "User Name"
$ git config --global user.email "email"

##### Applying colour to git
$ git config --global color.ui true

Git Config:
* global: User information, User-name and email.
* System: System has all user information who are linked with number of people.
* Local : Particular Project repository Information.
         --global 
         --system
         --local
Commands are: git config --global        (gets all global information)
              git config --global -e     (gets user name and Information)

Define or change username on git         (git config --global user.name "xyz555")

can replace or create user with email    (git config --global user.email "xyz@gmail.com")

##### Initializing a repository in an existing directory
If you’re starting to track an existing project in Git, you need to go to the project’s directory and type:
$ git init
This creates a new subdirectory named .git that contains all of your necessary repository files — a Git repository skeleton. At this point, nothing in your project is tracked yet.
To start version-controlling existing files you should start by tracking those files and do an initial commit. To accomplish that you should start with a few  `$ git add that specifies the files you want to track followed by a commit.
$ git add <file>
$ git add README
$ git commit -m 'Initial project version'


#### Checking the status of your files
The main tool you use to determine which files are in which state is the `$ git status` command. If you run this command directly after a clone, you should see something like this:
$ git status
# On branch master
nothing to commit (working directory clean)

### If you add a new file to your project, and the file didn't exist before, when you run a `$ git status` you should see your untracked file like this:
$ git status
# On branch master
# Untracked files:
# (use "git add <file>..." to include in what will be committed)
#
# README
nothing added to commit but untracked files present (use "git add" to track)

#### Staging files
After initializing a git repository in the chosen directory, all files will now be tracked. Any changes made to any file will be shown after a `$ git status` as changes not staged for commit.
To stage changes for commit you need to add the file(s) - or in other words, stage file(s).
# Adding a file
$ git add filename
# Adding all files
$ git add -A
# Adding all files changes in a directory
$ git add .
# Choosing what changes to add (this will got through all your changes and you can 'Y' or 'N' the changes)
$ git add -p
```
#### Committing files
After adding/staging a file, the next step is to commit staged file(s)
# Commit staged file(s)
$ git commit -m 'commit message'

# Add file and commit
$ git commit filename -m 'commit message'

# Add file and commit staged file
$ git commit -am 'insert commit message'

# Amending a commit
$ git commit --amend 'new commit message' or no message to maintain previous message

.................................................................................................................................................
Git branches:
                      A branch represents the independent line of development. The git branch commands lets you create, list, rename and delete the branches. The default name in Git is Master and in Git hub its is Main

    • To see the current branch  		: git branch -a
    • To add new branch            		: git branch branch_name
    • to switch branches             	: git checkout branch_name
    • To create and switch at a time 	: git checkout -b branch_name
    • To rename a branch 			    : git branch -m old new
    • To clone a specific branch 		: git clone -b branch_name repo-URL
    • TO delete a branch 			    : git branch -d <branch>
The -d option will delete the branch only if it is already been pushed and merged with the remote branch. Use -D instead if you want to force the branch to be deleted, even if it hasn’t been pushed or merged yet. The branch is now deleted locally.
```

#### Branching
# Creating a local branch
$ git checkout -b branchname

# Switching between 2 branches (in fact, this would work on terminal as well to switch between 2 directories - $ cd -)
$ git checkout 

# Pushing local branch to remote
$ git push -u origin branchname

# Deleting a local branch - this won't let you delete a branch that hasn't been merged yet
$ git branch -d branchname

# Deleting a local branch - this WILL delete a branch even if it hasn't been merged yet!
$ git branch -D branchname

# Remove any remote refs you have locally that have been removed from your remote (you can substitute <origin> to any remote branch)
$ git remote prune origin

# Viewing all branches, including local and remote branches
$ git branch -a

# Viewing all branches that have been merged into your current branch, including local and remote
$ git branch -a --merged

# Viewing all branches that haven't been merged into your current branch, including local and remote
$ git branch -a --no-merged

# Viewing local branches
$ git branch

# Viewing remote branches
$ git branch -r

# Rebase master branch into local branch
$ git rebase origin/master

# Pushing local branch after rebasing master into local branch
$ git push origin +branchname
..................................................................................................................................................
#### Git Merge:
                   If you want to merge branch-1 with branch-2 switch to branch-1(Master branch) first and give command 
    • git merge branch-2
No that command had merged the content of branch-1 and branch-2 
what ever the content is in branch-1 is now seen is branch-2 now

#### Merging branch to trunk/master
# First checkout trunk/master
$ git checkout trunk/master

# Now merge branch to trunk/master
$ git merge branchname

# To cancel a merge
$ git merge --abort

...................................................................................................................................................
#### Fetching and checking out remote branches (Origin) 
Origin: Default name of server/url is called as Origin
        Just give Origin instead of giving whole Url

# This will fetch all the remote branches for you.
$ git fetch origin

# With the remote branches in hand, you now need to check out the branch you are interested in, giving you a local working copy:
$ git checkout -b test origin/test

# Deleting a remote branch
$ git branch -rd origin/branchname
$ git push origin --delete branchname  or  $ git push origin:branchname

#### Updating a local repository with changes from a Github repository
$ git pull origin master


#### Tracking existing branch
$ git branch --set-upstream-to=origin/foo foo

To Push to Origin master
git push --set-upstream origin master

git push origin master/main

git remote add origin name_of_url     (To add remote repo of Origin)

git branch -M main
git push -u origin main
..................................................................................................................................................
#### Resetting
# Mixes your head with a give sha
# This lets you do things like split a commit
$ git reset --mixed [sha]

# Upstream master
$ git reset HEAD origin/master -- filename

# The version from the most recent commit
$ git reset HEAD -- filename

# The version before the most recent commit
$ git reset HEAD^ -- filename

# Move head to specific commit
$ git reset --hard sha

# Reset the staging area and the working directory to match the most recent commit. In addition to unstaging changes, the --hard flag tells Git to overwrite all changes in the working directory, too.
$ git reset --hard

...................................................................................................................................................

#### Git remote
# Show where 'origin' is pointing to and also tracked branches
$ git remote show origin

# Show where 'origin' is pointing to
$ git remote -v

# Change the 'origin' remote's URL
$ git remote set-url origin https://github.com/user/repo.git

# Add a new 'origin'
# Usually use to 'rebase' from forks
$ git remote add [NAME] https://github.com/user/fork-repo.git


###### Git Fork:
	    A fork is rough copy of a repository. Forking a repositoy allows you to freely test and debug with changes without affecting the original project.

...................................................................................................................................................
#### Stashing files
Git stash is a very useful command, where git will 'hide' the changes on a dirty directory - but no worries you can re-apply them later. The command will save your local changes away and revert the working directory to match the HEAD commit.
# Stash local changes
$ git stash

# Stash local changes with a custom message
$ git stash save "this is your custom message"

# Re-apply the changes you saved in your latest stash
$ git stash apply

# Re-apply the changes you saved in a given stash number
$ git stash apply stash@{stash_number}

# Drops any stash by its number
$ git stash drop stash@{0}

# Apply the stash and then immediately drop it from your stack
$ git stash pop

# 'Release' a particular stash from your list of stashes
$ git stash pop stash@{stash_number}

# List all stashes
$ git stash list

# Show the latest stash changes
$ git stash show

# See diff details of a given stash number
$ git diff stash@{0}
...................................................................................................................................................

# Squashing commits together
$ git rebase -i
This will give you an interface on your core editor:
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell

# Squashing commits together using reset --soft
$ git reset --soft HEAD~number_of_commits
$ git commit
** WARNING: this will require force pushing commits, which is OK if this is on a branch before you push to master or create a Pull Request.
..................................................................................................................................................

#### Git grep
# 'Searches' for parts of strings in a directory
$ git grep 'something'

# 'Searches' for parts of strings in a directory and the -n prints out the line numbers where git has found matches
$ git grep -n 'something'

# 'Searches' for parts of string in a context (some lines before and some after the grepped term)
$ git grep -C<number of lines> 'something'

# 'Searches' for parts of string and also shows lines BEFORE the grepped term
$ git grep -B<number of lines> 'something'

# 'Searches' for parts of string and also shows lines AFTER the grepped term
$ git grep -A<number of lines> 'something'
...................................................................................................................................................


#### Git blame
# Show alteration history of a file with the name of the author
$ git blame [filename]

# Show alteration history of a file with the name of the author && SHA
$ git blame [filename] -l

...................................................................................................................................................

#### Git log (To check History of commits)

# Show a list of all commits in a repository. This command shows everything about a commit, such as commit ID, author, date and commit message.
$ git log

# List of commits showing commit messages and changes
$ git log -p

# List of commits with the particular expression you are looking for
$ git log -S 'something'

# List of commits by author
$ git log --author 'Author Name'

# Show a list of commits in a repository in a more summarised way. This shows a shorter version of the commit ID and the commit message.
$ git log --oneline 
$ git log --oneline --graph --all


# Show a list of commits in a repository since yesterday
$ git log --since=yesterday

# Shows log by author and searching for specific term inside the commit message
$ git log --grep "term" --author "name"

...................................................................................................................................................
#### Git Diff (Checking what you are committing)
# See all (non-staged) changes done to a local repo
$ git diff

# See all (staged) changes done to a local repo
$ git diff --cached

# Check what the changes between the files you've committed and the live repo
$ git diff --stat origin/master
...................................................................................................................................................

#### Useful commands
# Check if a sha is in production
$ git tag --contains [sha]

# Number of commits by author
$ git shortlog -s --author 'Author Name'

# List of authors and commits to a repository sorted alphabetically
$ git shortlog -s -n

# List of commit comments by author
$ git shortlog -n --author 'Author Name'
# This also shows the total number of commits by the author

# Number of commits by contributors
$ git shortlog -s -n

# Undo local changes to a File
$ git checkout -- filename

# Shows more detailed info about a commit
$ git cat-file sha -p

# Show number of lines added and removed from a repository by an author since some time in the past.
$ git log --author="Author name" --pretty=tformat: --numstat --since=month | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }'

# Shows the log in a more consisted way with the graph for branching and merging
lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

...................................................................................................................................................
#### Useful alias
To add an alias simply open your .gitconfig file on your home directory and include the alias code

git config --global alias.s "git status"

git s (To check status as alias configured status as "s")

...................................................................................................................................................
### Getting & Creating Projects

| Command | Description |
| ------- | ----------- |
| `git init` | Initialize a local Git repository |
| `git clone ssh://git@github.com/[username]/[repository-name].git` | Create a local copy of a remote repository |

### Basic Snapshotting

| Command | Description |
| ------- | ----------- |
| `git status` | Check status |
| `git add [file-name.txt]` | Add a file to the staging area |
| `git add -A` | Add all new and changed files to the staging area |
| `git commit -m "[commit message]"` | Commit changes |
| `git rm -r [file-name.txt]` | Remove a file (or folder) |

### Branching & Merging

| Command | Description |
| ------- | ----------- |
| `git branch` | List branches (the asterisk denotes the current branch) |
| `git branch -a` | List all branches (local and remote) |
| `git branch [branch name]` | Create a new branch |
| `git branch -d [branch name]` | Delete a branch |
| `git push origin --delete [branch name]` | Delete a remote branch |
| `git checkout -b [branch name]` | Create a new branch and switch to it |
| `git checkout -b [branch name] origin/[branch name]` | Clone a remote branch and switch to it |
| `git branch -m [old branch name] [new branch name]` | Rename a local branch |
| `git checkout [branch name]` | Switch to a branch |
| `git checkout -` | Switch to the branch last checked out |
| `git checkout -- [file-name.txt]` | Discard changes to a file |
| `git merge [branch name]` | Merge a branch into the active branch |
| `git merge [source branch] [target branch]` | Merge a branch into a target branch |
| `git stash` | Stash changes in a dirty working directory |
| `git stash clear` | Remove all stashed entries |

### Sharing & Updating Projects

| Command | Description |
| ------- | ----------- |
| `git push origin [branch name]` | Push a branch to your remote repository |
| `git push -u origin [branch name]` | Push changes to remote repository (and remember the branch) |
| `git push` | Push changes to remote repository (remembered branch) |
| `git push origin --delete [branch name]` | Delete a remote branch |
| `git pull` | Update local repository to the newest commit |
| `git pull origin [branch name]` | Pull changes from remote repository |
| `git remote add origin ssh://git@github.com/[username]/[repository-name].git` | Add a remote repository |
| `git remote set-url origin ssh://git@github.com/[username]/[repository-name].git` | Set a repository's origin branch to SSH |

### Inspection & Comparison

| Command | Description |
| ------- | ----------- |
| `git log` | View changes |
| `git log --summary` | View changes (detailed) |
| `git log --oneline` | View changes (briefly) |
| `git diff [source branch] [target branch]` | Preview changes before merging |

------------------------------------------------------------------------------------------------------------------------------------------

yum install git -y
git --version

If you want to know how to install specific verison use github.com/git/git/releases
copy zip link and give wget and link 

The git developed in C language
