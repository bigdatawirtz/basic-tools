# Gitflows 

## A simple feature branch workflow for two

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

