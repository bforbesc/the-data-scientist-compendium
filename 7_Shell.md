# 🐚 shell scripting


- [Windows Command Prompt LS Equivalent Dir](https://skimfeed.com/blog/windows-command-prompt-ls-equivalent-dir/)
- [Awesome Bash](https://github.com/awesome-lists/awesome-bash): a curated list of delightful Bash scripts and resources.

General
```
pwd  
clear
~ # go back to home directory
-la # hidden stuff as well
cd 
ls -R -F # recursive, show all; indicate directory or runnable
cp # copy
mv second.txt third.txt # rename 
mv second.txt pasta\second.txt # move to new folder
rm # delete files
rmdir # delete folder
mdir cona\clitoris # create folder
cat # print file
man # describes function
cut # select columns
history # of commands used
! # select recently used command, can also use with index to history ex. !2
grep # selects lines according to what they contain
> # redirect output
wc # prints the number of characters, words, and lines in a file. You can make it print only one of these using -c, -w, or -l respectively
* # which means "match zero or more characters"
? # matches a single character, so 201?.txt will match 2017.txt or 2018.txt, but not 2017-01.txt
[...] # matches any one of the characters inside the square brackets, so 201[78].txt matches 2017.txt or 2018.txt, but not 2016.txt
{...} # matches any of the comma-separated patterns inside the curly brackets, so {*.txt, *.csv} matches any file whose name ends with .txt or .csv, but not files whose names end with .pdf
sort
^C # or CTRL + C to end process
$ # get the variable's value
$@ # all of the command-line parameters given to the script
$* # all arguments
$# # gives lenght(number) of arguments 
unzip # tool to unzip
| # use as input previous code
&& # run second command only if first one run sucessfully
; # run commands sequentially
sed # does pattern-matched string replacement
which bash # tells me where bash is
```

[Clone multiple repos from list](https://stackoverflow.com/questions/33649639/how-to-clone-a-list-of-git-repositories)
```
while read repo; do
    git clone "$repo"
done < projects.sh
```
Move data to a remote server
```
scp -r D:/0_PhD/0_Projects/3_HMR/Dados/hmr_data.csv bernardocosta@10.168.16.13:/media/data/bernardocostadata/HMR
```
Check connection to remote address
```
ping
```
See which ports are being used in server
```
htop
```
Keep server running
```
screen -ls  
screen -r
```
Rename folder
```
mv /home/user/temp /home/user/directory
```
Remove directory
```
rm -r "directory"
```
[Git: list files being tracked](https://stackoverflow.com/questions/15606955/how-can-i-make-git-show-a-list-of-the-files-that-are-being-tracked)
```
git ls-files
```


## Windows (CMD prompt)
```
cd 
dir /a
dir *.png
/?
../..
mkdir cona\clitoris
rmdir /s Bacon
del
move
copy
xcopy
tree
cls
echo "some text" > filename.txt
echo "add some text" >> filename.txtx\
ipconfig
wmic logicaldisk get name
attrib
dir > porky.txt
rename
set # get all variables
```
