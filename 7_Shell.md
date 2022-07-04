# 🐚 shell scripting


- [Windows Command Prompt LS Equivalent Dir](https://skimfeed.com/blog/windows-command-prompt-ls-equivalent-dir/)
- [Awesome Bash](https://github.com/awesome-lists/awesome-bash): a curated list of delightful Bash scripts and resources.

General
```shell
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
```shell
while read repo; do
    git clone "$repo"
done < projects.sh
```
Move data to a remote server
```shell
scp -r D:/0_PhD/0_Projects/3_HMR/Dados/hmr_data.csv bernardocosta@10.168.16.13:/media/data/bernardocostadata/HMR
```
Check connection to remote address
```shell
ping
```
See which ports are being used in server
```shell
htop
```
Keep server running
```shell
screen -ls  
screen -r
```
Rename folder
```shell
mv /home/user/temp /home/user/directory
```
Remove directory
```shell
rm -r "directory"
```

## Windows (CMD prompt)
```shell
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

## Setting up environment
[How to change the Jupyter start-up folder in your device](https://stackoverflow.com/questions/35254852/how-to-change-the-jupyter-start-up-folder) 
1. Run ```jupyter server --generate-config``` in ```cmd``` (or Anaconda Prompt)
2. Navigate to ```C:\Users\username\.jupyter\jupyter_notebook_config.py``` 
3. Replace ```#c.ServerApp.root_dir = ''``` with ```c.ServerApp.root_dir = '/the/path/to/desired/folder/'```

```shell
conda create --name "env_name" jupyterlab pandas seaborn scikit-learn

conda activate "env_name"

conda install -c anaconda ipykernel  
ipython kernel install --user --name="name to show on jupyterlab"
```

Base set up: install a package for kernel management in your base environment 
```shell
conda install nb_conda_kernels
conda config --add channels conda-forge
```

Manage jupyter kernels
```shell
jupyter kernelspec list 
jupyter kernelspec uninstall kernel_name
```

Manage jupyter notebook sessions
```shell
jupyter notebook list 
jupyter notebook close 8889
```

Other Conda commands
Check if a specific package is installed
```shell
conda list -n <environment name> <package name>
conda upgrade <package name>
```
Install a package with a specific version
```shell
conda <package name> = <version number>
conda remove <package name>
conda deactivate
conda env remove -n mlcourse --allconda 
```
