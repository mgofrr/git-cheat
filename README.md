## Git


### Git Flow Step Guide

    # creating a new branch from developer
    git checkout developer
    git pull --rebase                      
    git checkout -b feature/new-changes    
    
    # adding your changes
    git add .
    git commit -m 'adding new changes'
    git push origin feature/new-changes
    
    # rebase from developer branch
    git checkout developer
    git pull --rebase                 # --rebase to least resistance
    git checkout feature/new-changes
    git rebase developer                  
    
    # solving conflicts (if needed)
    git rebase --continue             # do this until you solve all conflicts
    git rebase --skip                 # do this when you finish to solve conflicts

    hint: Use 'git am --show-current-patch' to see the failed patch
    Resolve all conflicts manually, mark them as resolved with "git add/rm <conflicted_files>", 
    then run "git rebase --continue".

    You can instead skip this commit: run "git rebase --skip".
    To abort and get back to the state before "git rebase", run "git rebase --abort".

    # update your remote branch
    git push origin feature/new-changes --force-with-lease

    # merging remote branches
    git checkout developer
    git merge --no-ff feature/new-changes # let the default commit comment

    # update the remote developer branch
    git push origin developer 


--- 

### Managing releases

    # create a new annotated tag
    git tag -a v1.0.0 -m "Releasing version v1.0.0"
    # or create a simple tag
    git tag v1.0.0

    # publish tag
    git push origin v1.0
    # or publish all tags
    git push --tags  

    # list tags
    git tag -l -n3

    # show tags details
    git show v1.0.0

    # edit tag
    git tag -a -f v1.0.0 <commit_id>

    # delete tag
    git tag -d v1.0.0


--- 

### Comparing with diff

    # show changes in code:
    git diff master origin/master

    # compare nth last commit:
    git diff {branch~20,branch}:<filename> 

    # show commits that haven't been merged into local branch:
    git cherry master origin/master

    # commits on remote branch since when local branch was created:
    git diff HEAD...origin/master

    # to see the differences of what you have on your local branch
    #	but that does not exist on remote branch run:
    git diff origin/master...HEAD

    # add any remote repositories you want to compare:
    git remote add foobar git://github.com/user/foobar.git

    # compare any branch from your local repository to any remote you've added:
    git diff master foobar/master


--- 

### Discard Changes

    # first of all update your local copies:
    git fetch 
    # fetch won't change your working copy.

    # unstage the file to current commit (HEAD)
    git reset HEAD <file>

    # unstage everything - retain changes
    git reset

    # discarding changes to specific file
    git checkout  -- <filename>
    git checkout origin/master -- <filename> 	 #specific branch
    git checkout <commit> <filename>

    # overwrite all changed files:
    git reset --hard origin/master


--- 

### Stash

    # give a name to your changes:
    git stash save "my_stash"

    # list down all your stashes:
    git stash list

    # apply a stash and remove it from the stash stack:
    git stash pop stash@{n}

    # apply a stash and keep it in the stash stack, type:
    git stash apply stash@{n}

    # restore a specific file from stash:
    git restore -s stash@{0} -- <filename>


--- 

### Merging

#### Merging with stash

    # This is the path to least resistance with git

    # stash your local changes
    git stash

    # update the branch to the latest code
    git pull

    # merge your local changes into the latest code
    git stash apply

    # proceed to add, commit and push your changes
    git add
    git commit
    git push


#### Merge a git branch into master:

    git checkout master
    git pull origin master
    git merge test
    git push origin master


#### Merging changes from master into my branch:

    git pull
    git checkout custom_branch
    git rebase master
    # This will update custom_branch with changes from master branch.
   

#### This is also possible with
    
    git checkout custom_branch
    git merge master


#### Reset a remote branch to remote master

    git checkout develop
    git merge --no-commit master
    git checkout --theirs master .
    git commit
    git push origin develop


--- 



