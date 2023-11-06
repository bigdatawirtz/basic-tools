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

Branches
* ...

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


## GitHub

GitHub is a platform and cloud-based services for software development and version control using Git. It provides repositories for software developers.

### Github first steps

How to clone a repository from Github, add changes locally and send them back to the remote repository.

1. Clone the remote repository: `git clone https://github.com/some_github_user/repo-name.git`
2. Enter the local repo directory: `cd repo-name`
3. Add new files or update existing ones
4. Add changes to *Stage Area*: `git add .`
5. Confirm changes in *Stage Area* to *Repository*: `git commit -m "comment"`
6. Send changes to remote repository: `git push`

The `git push` command requires authentication. You need to create an authentication token in the Github web to use as a password in each push operation.