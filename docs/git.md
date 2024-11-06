Git is a control version software (CVS).

## Commands

Basic commands

* `git init`: Initialize a local repository in current directory.
* `git add .`: Add all modified files from current directory to the stage area.
* `git commit -m`: Commit all changes in current stage area to the repo.
* `git status`: Show the working tree status
* `git log`: Show commit logs
* `git checkout commit-id`: Moves to the indicated commit

Remote repositories

* `git clone [repo-url]`: Clone remote repository in local filesystem.
* `git push`: Upload changes to remote repository
* `git pull`: Download and integrate remote changes into local repository

Configuration

* `git config --list`: Show current configuration
* `git config var-name=var-value`: Set a value for the indicated config variable



## Git first steps tutorial

1. Create a new directory to host a repository: `mkdir new-repo`
2. Initialize new repo: `git init`
3. Update configuration (if needed): `git config user.name=myname` + `git confit user.email=my-email@domain.com`
4. Verify my current configuration: `git config --list`
5. View repo status: `git status`
6. Create a new file: `echo Hi > greetings.txt`
7. View new status: `git status`
8. Add new file to staging area: `git add greetings.txt`
9. Commit changes to repository: `git commit -m 'changes added' `
10. View status:  `git status`
11. View history log: `git log`
12. Create a new file: `echo Bye > goodbye.txt`
13. View new status: `git status`
14. Add new file to staging area: `git add goodbye.txt`
15. Commit changes to repository: `git commit -m 'new file added' `
16. View status:  `git status`
17. View history log: `git log --oneline`
18. List files: `ls`
19. Move to previous state: `git checkout commit-id`
20. Verify current files in working directory: `ls`
21. View history log: `git log --oneline --all`
22. Back to the future: `git checkout more-recent-commit-id`

## Git branches and merge

You can use branches to manage many lines of develpment independently. To incorporate the content of a new branch in the main branch you have the merge function.

* `git log --oneline --graph`; this combination can be useful to understand branches.
* `git branch newbranch`: create a new branch called newbranch
* `git branch`: view branches
* `git switch newbranch`: switches to newbranch
* `git merge newbranch`: merge newbranch in the current branch

### Merge Fast-Forward

When you create a new branch and you make many commits you can merge this branch into main. If main doesn't have any commits since the new branch creation the merge function will use the Fast-Forward technique. 

1. (main) > `git branch newbranch`
2. (main) > `git switch newbranch`
3. (nova_branch) > `touch file1.txt`
4. (nova_branch) > `git add .`
5. (nova_branch) > `git commit -m "file.txt added"`
6. (nova_branch) > `switch main`
7. (main) > `git merge nova_branch`

### Merge Three Way (without conflicts)

Merge Three Way without conflicts happen when you merge a new branch with commits and the main branch with commits too. If the commits of the two branches don't involve the same files then there won't be any conflitcs. The merge is automatic.

1. (main) > `git branch newbranch`
2. (main) > `git switch newbranch`
3. (nova_branch) > `touch file1.txt`
4. (nova_branch) > `git add .`
5. (nova_branch) > `git commit -m "file.txt added"`
6. (nova_branch) > `git switch main`
7. (main) > `touch file2.txt`
8. (main) > `git add .`
9. (main) > `git commit -m`
10. (main) > `git merge nova_branch`


### Merge Three Way (with conflicts)

Merge Three Way without conflicts happen when you merge a new branch with commits and the main branch with commits too. If the commits of the two branches involve the same files then there will be conflitcs. The merge is not automatic and the user have to decide wich code to save and commit.

1. (main) > `git branch newbranch`
2. (main) > `git switch newbranch`
3. (nova_branch) > `echo "pan" > lista_compra.txt`
4. (nova_branch) > `git add .`
5. (nova_branch) > `git commit -m "pan added"`
6. (nova_branch) > `switch main`
7. (main) > `echo "queixo" > lista_compra.txt`
8. (main) > `git add .`
9. (main) > `git commit -m`
10. (main) > `git merge nova_branch`
11. Git stops the merge operation and ask the user to resolve the conflicts
12. `nano lista_compra.txt`
13. (main) > `git add lista_compra.txt`
14. (main) > `git commit -m "lista da compra completa"`


## GitHub

GitHub is a platform and cloud-based services for software development and version control using Git. It provides repositories for software developers.

### Github first steps

How to clone a repository from Github, add changes locally and send them back to the remote repository.

1. Clone the remote repository: `git clone git@github.com:some_github_user/repo-name.git`
2. Enter the local repo directory: `cd repo-name`
3. Add new files or update existing ones
4. Add changes to *Stage Area*: `git add .`
5. Confirm changes in *Stage Area* to *Repository*: `git commit -m "comment"`
6. Send changes to remote repository: `git push`

The `git push` command requires authentication. You need to create an authentication token in the Github web to use as a password in each push operation.

### SSH Authentication

You can user your RSA SSH public key to authenticate in Github:

1. Confirm that you're using the right remote: `git remote -v` . Are your remotes pointing to git@github:username/reponame.git ?
2. Go to your Profile Settings and paste your public RSA public Key in the 'SSH and GPG keys' (New SSH key button).
3. Git will use your default RSA Key in your next `push` operation.

### Github flows

When you code with more people you need to stablish certain rules to coordinate work, this is called a *workflow*. The are many different workflows, for example:

* Feature Branch Workflow: Each new feature or fix should be developed in its own branch. When the feature is complete it gets merged into master (or main). This workflow is good for small teams and projects with few contributors.
* Gitflow Workflow: It's a more complex workflow that includes multiple branches to support features, releases and hotfixes.

We suggest the following simplified version of the Feature Branch Workflow

#### A simple feature branch workflow for two

Create repository on GitHub

Clone repository locally

Time to work!

Create your own branch (`git branch new_branch`)  
Switch to your branch (`git switch new_branch`)  
Work + Commit + Work + Commit...  
Return to main (`git switch main`)  
Check if there’s anything new on GitHub and bring it to main (`git pull`)  
Merge your branch into main (`git merge new_branch`)  
Push updated changes to GitHub (`git push`)

Back to “Time to work!”

**Note**: Each time, we use a different branch name: `new_branch1`, `new_branch2`, ...

If you want, you can push your local branch to the remote repository if it isn't ready to merge with main. The first time you do this you'll have to make a `git push --set-upstream origin new_branch`. Then just use `git push` for subsequent pushes.

