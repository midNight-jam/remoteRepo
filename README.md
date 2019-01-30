# remoteRepo
git excercise


git commands

///////////////////////
//// Fundamentals
///////////////////////

#1 for Version :  

> git --version

------

#2 Setting the config values : 

> git config --global user.name "Jayam Malviya"
> git config --global user.email "malviya.jayam@gmail.com"

getting the list of set config values

> git config --list

------

#3 Help

> git help configName
> git configName --help

------

#4 Initializing a remote repo from the exsisting code

from the source dir

> git init 				(creates a ".git" dir that maps our project with git)

------

#5 for getting the status of your local repo

> git status

------

#6 Creating a .gitignore file for ignoring the files from git to track.

> touch .gitignore 			(creates the empty .gitignore file)

add all the file names or reg expression to ignore the files.

------

#7 Adding files to the staging area.

> git add -A

-A = all (adds even the untracked files!)

------


#8 Removiing the files from staged area.

> git reset <filePath> 		(removes the file from the stage area)

> git reset  				(removes all the staged files)

------

#9 Commiting the changes

> git commit -m "commit message" 

commits the staged files locally

------

#10 Commit logs

> git log 				(get the commit log in default view)


> git log --pretty=oneline 		(get the commit log in oneline view)

------

#11 Clone repo locally

> git clone <clone URL> 

------

#12 Viewing the information about the remote repo

> git remote -v 		(gets the info about the remote repo)

> git branch -a 		(get all the branches present for this repo)

------

#13 Push & Pull

> git push origin master

> git pull origin master

------

#14 Create a branch for feature

> git branch calc-divide  		(creates the branch locally)

> git checkout calc-divide   	(switch to the newly created branch)

> git branch   					(logs all the branches present on local)

------

#15 After commit push branch to remote

> git push -u origin calc-divide	(pushes the branch to remote)

------


#16 Merge a branch (merge calc-divide to master)

> git checkout master		(first switch to master)

> git pull origin master 	(get the latest on master)

> git branch --merged		(to get the list of merged branches to master)

> git merge calc-divide		(merge the calc-divide branch to master locally)

> git push origin master	(push the merged master to remote)

------


#17 Deleting a branch after it has been merged (delete calc-divide from remote)

> git branch -d calc-divide				(delete branch locally)

> git branch -a 						(confirm that the branch has been deleted locally)

> git push origin --delete calc-divide	(delete the branch at remote)

> git branch -a 						(confirm that the branch has been deleted remotely)

------


#18 To bring a modified file to the current state from repo & loose ur changes

> git checkout <filePatName>	(removes ur changes on the file & gets the latest from remote repo)

------


#19 To change your last commit message

> git commit --amend -m "new message"		(completely replace the old message with the new one)

> git commit --amend		(opens up VI edit message)

> git commit --amend	--no-edit (amend without changing the commit message)


Also, observe that after you have changed the commit message the commit HASH also changes, because the commit message is part of the HASH. And when the HASH changes that means the git history changes. Thus, we want to do it only for the changes owned by us. We shouldnt changes history for the changes which other people have already pulled.

------


#20 To view the changes included in your last commit

> git log --stat (gives the details of the changes in the commit)

------

#21 CherryPick, get your commit from one branch to another

> git cherry-pick <commitHASH>		(brings the changes in the commit to current branch)


CherryPick doesnt deletes the commit from the original branch, to do so use git reset.
------



#22 git reset

> git reset --soft <HASH>

soft will reset us to the commit that we have specified, but it will keep the changes in the staging area.

> git reset --mixed / default (no option) <HASH>

mixed will reset us to the commit that we have specified, but it will keep the changes in the working dir & NOT in the staging area.


> git reset --hard <HASH>

Will make all of our tracked files match the state they were in at the HASH that we specified, be careful cuz it will get rid of your changes.
But leaves the untracked files untouched.

------


#23 Get rid of the Untracked Files

> git clean -df 

d : for untracked dir
f : for untracked files

------


#24 Get changes back from git reset --hard

We can be out of luck, if a lot of time has passed since we ran the git reset, because git garbage collects them (30 days).

> git reflog  

Shows the commit in the order in which we last referenced them, a walkthrough of what we have been doing.  

Grab the HASH before the reset & use checkout

git checkout <HASH>


This leaves us in a detached Head state, means that we are not currently on a branch and this point will be trashed in future. So create a branch with this recovered backup. Now from that branch we can cherry pick the changes & bring it your branch for commit.

------


#25 Revert

To undo some commit that other people have already pulled the changes.
Revert creates new commit, to reverse the effect of an earlier commit.
Its not going to modify or delete the exsisting commits, thus no rewriting the history. 

> git revert <HASH>

It will create a new commit that reverts the commit that we specified. 

------


#26 git diff between commits

> git diff <HASH1> <HASH2>


Also, observe that after you have changed the commit message the commit HASH also changes, because the commit message is part of the HASH. And when the HASH changes that means the git history changes.

------


#27 git Stash

stash the changes in to seperate place, they get carried over from branch, so stash is indepenedent of branches. 

> git stash save "message"

> git stash list 	(will have stashes with IDs)

> git stash apply <STASHID>

doesnt remove changes from the stash

> git stash pop

applies the changes and drop the stash

> git stash drop <STASHID>

drops the changes from the stash list

> git stash clear 

drops all the changes from the stash list 

------


#28 git add

> git add -A (default behavior for git add)

Stage all of the changes (modofied, deleted, new) in the entire working tree, regardless of where you fire this cmd from.

> git add -A <dirpath> 	

adds only the changes found below this dir

> git add -u (update)

entire changes for the tracked files, but none for the untracked changes

> git add .	(current dir)


> git stash drop <STASHID>

drops the changes from the stash list

> git stash clear 

drops all the changes from the stash list 

------

#29  Temporarily stop tracking changes to file

This will tell git you want to start ignoring the changes to the file

 > git update-index --assume-unchanged path/to/file

When you want to start keeping track again

 > git update-index --no-assume-unchanged path/to/file


------

#30  To check for unpushed changes

> git log origin/master..HEAD

> git diff origin/master..HEAD


------

#31  To cache your credentials, here we are caching it for 1000 hrs

> git config credential.helper 'cache --timeout=60000'

------

#32  To get history of the file (includes renames)

> git log --follow <path/to/fileName>

------

#33  To get url from which the repository was downloaded

> git config --get remote.origin.url

------

#34  To get the current commit hash of local head

> git show HEAD 

------

#35  To get the changes done on a single file via two commits

> git diff hash1..hash2 -- filepath

------

#36  To rename dir/file changes in git

> git mv _old name_    _new name_

------

#37 Show contents of stash

> git stash show -p stash@{1}

------

#38 List stash with creation time

> git stash list --date=local

------

#39 reset to a particular commit id

> git reset --hard commitHash

------

#40 to create new alaises 
 edit the .gitconfig file and add a new section of [alias], each line begins with an alias.Refer : https://git.wiki.kernel.org/index.php/Aliases. Below are mine
 
 
 	[alias]
	
	logo = log --oneline -30
 
	logoo = log --oneline -100
 
	lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative -30
 
	st = status
 
	ci = commit
 
	br = branch
 
	co = checkout
 
	df = diff
 
	dc = diff --cached
 
	lg = log -p
 
	who = shortlog -s --
 
	sthl = stash list

#41 update a single file from remote of a branch

use git checkout <remote/branchName> -- path/to/file

fetch will download all the latest changes, but will not put in your work area(current checked out code).

checkout will update the uopdate particular file in the working tree from the downloaded changes

> git fetch

> git checkout origin/master -- path/to/file
