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
