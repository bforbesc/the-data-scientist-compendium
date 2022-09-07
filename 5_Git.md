# [![My Skills](https://skills.thijs.gg/icons?i=git)](https://skills.thijs.gg) git

## Resources
- [The official git documentation](https://git-scm.com/docs)
- [Pro Git book](https://git-scm.com/book/en/v2): the official git book
- [A visual cheatsheet](https://ndpsoftware.com/git-cheatsheet.html#loc=local_repo;)
- [Additional cheatsheets](https://training.github.com/)

## Snippets
### Everything starting with ```git <...>```:

Initiate git and check the current version:
``` shell
init # start tracking folder
--version
remote add origin 'your_url' # remote repository for your local repository
clone 'your_url' # clone an existing GitHub repository
```

Common operations:
```shell
status
add 'your_file' # or 'add .' to add everything in your folder being tracked
reset HEAD 'your_file' # remove file from stage area
commit -m 'your message'
commit -am 'your message' # commit directly without stage area
push # uploads all local branch commits to GitHub
pull # updates current local working branch with all new commits from the corresponding remote branch on GitHub (combination of 'fetch' and 'merge')
```
*Note: commit messages should not exceed 50 characters and should explain what was changed and why the change was made*

Check and configure user information:
```shell
config --list
config --global user.email 'your_email@email.com'
config --global user.name 'your_user_name'
```

Version control:
```shell
log # show commit logs
log -author = 'your name'
diff  # compares work copy and repository
diff --stage # compares stage area and repository 
checkout -b # gets version of repository
checkout 'your_commit_ID' --'your_file_name' # gets version by commit ID
```

[List files being tracked](https://stackoverflow.com/questions/15606955/how-can-i-make-git-show-a-list-of-the-files-that-are-being-tracked)
```
ls-files
```

[Stop tracking files or folders](https://stackoverflow.com/questions/1274057/how-do-i-make-git-forget-about-a-file-that-was-tracked-but-is-now-in-gitignore)
```shell
rm -r --cached <folder>
```

[Adding a local repository to GitHub](https://docs.github.com/en/get-started/importing-your-projects-to-github/importing-source-code-to-github/adding-locally-hosted-code-to-github)
```shell
init -b main
add . # Adds the files in the local repository and stages them for commit. To unstage a file, use 'git reset HEAD YOUR-FILE'.
commit -m "First commit" # Commits the tracked changes and prepares them to be pushed to a remote repository. To remove this commit and modify the file, use 'git reset --soft HEAD~1' and commit and add the file again.
remote add origin  <REMOTE_URL> # Sets the new remote
remote -v # Verifies the new remote URL
branch -M main
push -u origin main # Pushes the changes in your local repository up to the remote repository you specified as the origin
```
[How to delete a Git repository](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/delete-local-git-repository-repo-command-windows-linux-rm)
```shell
 rm -fr .git
 ```
