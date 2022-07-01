# Git

Everything starting with "git"...
```
init
--version
config --list
config --global user.email "bernardoforbescosta@gmail.com" 
config --global user.name "bforbesc"
status
log
log -author="Bernardo Forbes Costa"
diff  # compares work copy and repository
diff --stage # compares stage area and repository 

checkout -b # gets version of repository
checkout 01e7dba -- pixa.txt # gets version by commit ID
add pixa.txt  # or "add ." to add everything in that folder
reset HEAD file.txt # remove from stage area
commit -m "Commit message"
commit -am "Commit message" # commit directly without stage area

remote add github_ninckname_project https://github.com/Data-Science-Knowledge-Center-Nova-SBE/doca-pesca-model.git
push origin file_name
push -u github_ninckname_project master
fetch
clone https://github.com/Data-Science-Knowledge-Center-Nova-SBE/doca-pesca-model.git 
pull origin master
```

---
