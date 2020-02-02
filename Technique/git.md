## git commit

git config --global core.editor /usr/bin/vim

## git commands

合并一个分支的之前提交的内容到另一个分支，可以将这个分支reset --soft HEAD^到之前要合并的一个版本，然后合并

git checkout master // switch branch  
git reset --soft HEAD^ // Undo a commit  
git checkout dev  
git merge master // merge branch master to current branch

git revert HEAD~3

References  
https://git-scm.com/docs/git-reset#git-reset-Undoacommitandredo  
https://git-scm.com/docs/git-merge

## git config --list
