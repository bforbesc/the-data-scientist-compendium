# [![My Skills](https://skills.thijs.gg/icons?i=git)](https://skills.thijs.gg) git

Everything starting with ```git <...>```:
```
init
--version
```

```
status
commit -m "Commit message"
commit -am "Commit message" # commit directly without stage area
push origin file_name
push -u github_ninckname_project master
```

```
config --list
config --global user.email "bernardoforbescosta@gmail.com" 
config --global user.name "bforbesc"
```
```

log
log -author="Bernardo Forbes Costa"
diff  # compares work copy and repository
diff --stage # compares stage area and repository 
checkout -b # gets version of repository
checkout 01e7dba -- pixa.txt # gets version by commit ID
```

```
add pixa.txt  # or "add ." to add everything in that folder
reset HEAD file.txt # remove from stage area
remote add github_ninckname_project https://github.com/Data-Science-Knowledge-Center-Nova-SBE/doca-pesca-model.git
fetch
clone https://github.com/Data-Science-Knowledge-Center-Nova-SBE/doca-pesca-model.git 
pull origin master
```
[Git: list files being tracked](https://stackoverflow.com/questions/15606955/how-can-i-make-git-show-a-list-of-the-files-that-are-being-tracked)
```
git ls-files
```

See [cheatsheet on Git](https://education.github.com/git-cheat-sheet-education.pdf) and the course I taught on [Advanced Programming for Data Scince](https://gitlab.com/adpro1/adpro2022/classes-advanced-programming-2022/-/tree/master/git_demo) for more.
