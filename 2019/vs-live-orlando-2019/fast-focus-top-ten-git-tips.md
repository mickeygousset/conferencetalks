# Top Ten Git Tips (actually more like 30 tips) in 20 minutes

## Setup (do this as part of the talk, when it starts)
- Open Git Bash shell
- cd ../../Repos (location of my repos)
- mkdir orlando2019

## Tip #1: Get Started With A New Repo
- git init
- I'm on the master branch
- ls -al ===> there is a folder called .git that was created

## Tip #2: What Is This .git Folder
- ls -al .git
- This folder is what make this a "git" repository. It stores the metadata and object database for the project, including:
  - Remote information (which remote server your project is connected to)
  - History of all local commits
  - Branch information (on which branch your current project state (HEAD) is pointing to)
  - Logs of all local commits you have made (including reverted changes)
- Review Of Items In .git Folder
  - Config - This is the local config file for the repository
  - Description - text file with description of repository, usually surfaced in web gui, can also be read by hook scripts
  - HEAD - reference to the current branch that HEAD is pointing to
  - Hooks - scripts that can be run when different things happen in the repo
  - Info - Exlude file for ignored patterns
  - Objects - Objects database where files will be stored.  two letter SHA1 folders with 38 character file names containg the objects. Compressed and encrypted
  - Refs
    - Heads - used for branches
    - Tags - each file here corresponds to the tag previously created using the git tag command

## Tip #3-6: git config
- You can't issue a commit command without first configuring your name and email address
- git config --list
- System -> Global -> Local
  - System ==> ming\etc folder in the gitconfig file
  - Global ==> .gitconfig stored in user's profile
  - Local ==> .git/config
- git config --global --list
- Mention core.editor and why you might want to change it
  - git config --global --core.editor

## Tip #7: git add
- Create some files
  - echo "a" > a.html
  - echo "b" > b.html
  - echo "c" > c.html
- You may not want to commit every file you create to source control. Before you commit to a git repo, you need to explicitly identify which files to group together as part of the commit. This is called "staging" the file
- git status
- git commit ==> Notice it says untracked files present. Have to stage before you can commit
- git add a.html
- git add c.html
- git status
- git add . ==> adds all changed files, foldes, and subfolders

## Tip #8: git status
- Gives you an idea of what is going on in your working tree. Tells you what branch you are on, which files you've staged, and which files are untracked
- git status
- git status --verbose

## Tip #9-11: git commit
- Committing permanently (sort of) saves changes to the git repository
- all commits must have a message, and are tracked via user name and email address of the person making the commit
- git commit -m "First Commit. Adding three files
- git status
- echo "a" >> a.html
- git status
- git add .
- git status
- echo "bbb"  b.html
- git status
- git commit -a
- This opens my default editor, in this case VSCode. I can use this to write a more detailed git commit message
- git status ==> There is nothing to show right now
- I could also use: git commit -am "message"
- li -al .git/objects and see the folders
- look in objects folder

## Tip #12-15: Branching 101
- git branch ==> list of all local branches
- git branch -a ==> list of all local branches and remote branches
- git checkout -b my_first_branch ==> creates a new local branch and changes to it
- echo "d" > d.html
- git branch ==> shows the two branches, and which one I'm active one
- git add d.html
- git commit -m "adding d.html to my_first_branch"
- git checkout master ==> you will notice the file isn't there (d.html)
- git merge my_first_branch
- git branch -D my_first_branch

## Tip #16-22: git log
- git log ==> shows you everything
- git log -n 2 ==> shows you the last two commits
- git log --grep "first"
- git log --oneline
- git log -p --stat ==> shows the files and statistics
- git log --graph
- git checkout -b my_second_branch
- echo "e" > e.html
- git add .
- git commit -m "e.html"
- git checkout master
- git merge my_second_branch
- git log --graph --all --oneline --decorate

## Tip #22.5
- alias
- git config --local alias.mylog 'log --graph --all --oneline --decorate"


## Tip #23-24: Deleting A File
- git status
- ls -la
- git rm a.html ==> removes the files from the repo and also deletes it from the local file system
- git status
- ls -la
- git rm --cached b.html ==> Removed from repository but not from file system
- git commit -m "removing files from system"
- git status
- a.html is gone, b.html is still there.

## Tip #25: Undoing Changes - Saving Changes For Later - Stash
- Stash allows you to put things in a drawer for later. For example: you are working on something but suddenly you need to change branches to create a hotfix for an urget bug.
- echo "cc" > c.html
- git add c.html
- git status ==> will show C as staged and B as untracked
- git stash -u ==> will save every untracked file, staged, and unstaged modifications
- git stash list
- git stash show
- git status
- git stash pop ==> will retrieve the latest stash and delete it
- git stash list
- git status

## Tip #26: Undoing Changes - Add Something To Latest Commit - Amend
- Amend allows you to add more files to the latest commit. Use case: You forgot to stage a certain file that should have been part of the commit. Even with no file you can still commit with the "Amend" option to change the message
- git commit -am "commiting my changes"
- git add b.html
- git log -p
- git commit -amend -m "adding b.html and modifying commit message"
- git commit --amend -m "adding b.html and modifying commit message"
- git log --oneline
- git log -p


## Tip #27: Unstaging Changes (precommit) - reset
- This simply unstages the c.html and puts the changes back into your working tree. Use case: Out of habit, you staged all the modifications using git add ., but you want to unstage certain files and commit them separately.
- echo "ccc" > c.html
- git status
- git add .
- git status
- git reset .
- git status
- I could also have said: git reset c.html


## Tip #28: Remove new/untracked files and directories
- echo "f" > f.html
- git clean -i
- Interactively walk through the process




## Tip #29: More with reset
- maybe, if needed
- 

https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified
<br>
https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting
<br>
https://www.poftut.com/how-to-reset-git-head/