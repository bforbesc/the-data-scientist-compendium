# Table of contents
1. [Resources](#resources)
2. [Bash snippets](#bash-snippets)
3. [Windows command prompt snippets](#windows-command-prompt-snippets)
4. [Anaconda/ Conda snippets](#anaconda-conda-snippets)


# Resources
- [Awesome Bash](https://github.com/awesome-lists/awesome-bash): a extremely comprehensive list of Bash scripts and resources
- [Windows commands official documentation](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands#r)
- [Windows Command Prompt vs. Shell equivalence of commands](https://skimfeed.com/blog/windows-command-prompt-ls-equivalent-dir/)
- [Conda: Myths and Misconceptions](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/?utm_source=pocket_mylist)
- [How to use tmux](https://www.howtogeek.com/671422/how-to-use-tmux-on-linux-and-why-its-better-than-screen/)
- [VS Code and ```tmux``` intergation](https://cppdev.medium.com/vs-code-and-tmux-intergation-for-reliable-remote-development-e26594e6757a)
- [Details on ```screen```](https://linuxize.com/post/how-to-use-linux-screen/)
- [Using pip with Conda](https://www.anaconda.com/blog/using-pip-in-a-conda-environment):
    - Use an isolated conda environment. 
    - Only after conda has been used to install as many packages as possible should pip be used to install any remaining software. 
    - If modifications are needed to the environment, it is best to create a new environment rather than running conda after pip. 
    - When appropriate conda and pip requirements should be stored in text files.


# Bash snippets
General commands
```shell
-la # show hidden files
ls -R -F # recursive, show all; indicate directory or runnable
cp # copy
mv second.txt third.txt # rename file
mv /home/user/temp /home/user/directory # rename folder
mv second.txt pasta\second.txt # move to new folder
rm # delete files
rm -r 'directory' # delete directory
rmdir # delete folder
mdir parent\child # create folder
cat # print file
man # describes function
cut # select columns
history # history of commands used
sort
unzip # tool to unzip
^C # or CTRL + C to end process
which bash # tells me where bash is
```

[Determine size of files or folders](https://stackoverflow.com/questions/11720079/linux-command-to-get-size-of-files-and-directories-present-in-a-particular-folde)
```shell
ls -l filename   # Displays Size of the specified file
ls -l *          # Displays Size of All the files in the current directory
ls -al *         # Displays Size of All the files including hidden files in the current directory
ls -al dir/      # Displays Size of All the files including hidden files in the 'dir' directory

du -sh directory_name    # Gives you the summarized(-s) size of the directory in human readable(-h) format
du -bsh *                # Gives you the apparent(-b) summarized(-s) size of all the files and directories in the current directory in human readable(-h) format
```

[Determine number of cores](https://linuxhint.com/find-the-number-of-cores-in-ubuntu/)
```shell
nproc
```

[Remove all files from directory](https://askubuntu.com/questions/60228/how-to-remove-all-files-from-a-directory)
```shell
rm *
```

[Decompress file with .zst or tar.zst extension](https://stackoverflow.com/questions/45355277/how-can-i-decompress-an-archive-file-having-zst-or-tar-zst)
```shell
tar --use-compress-program=unzstd -xvf file_name.tar.zst
```

[Check user's activity in server](https://www.golinuxcloud.com/list-check-active-ssh-connections-linux/)
```shell
who
w
```

[Determine shell in use](https://www.cyberciti.biz/tips/how-do-i-find-out-what-shell-im-using.html)
```shell
printf "My current shell - %s\n" "$SHELL"
```

General operators
```shell
~ # go back to home directory
! # select recently used command, can also use with index to history ex. '!2'
> # redirect output
| # use as input previous code
&& # run second command only if first one run sucessfully
; # run commands sequentially
* # all items/ "match zero or more characters"
? # matches a single character, so 201?.txt will match 2017.txt or 2018.txt, but not 2017-01.txt
$ # get the variable's value
$@ # all of the command-line parameters given to the script
$* # all arguments
$# # gives lenght(number) of arguments 
[...] # matches any one of the characters inside the square brackets, so 201[78].txt matches 2017.txt or 2018.txt, but not 2016.txt
{...} # matches any of the comma-separated patterns inside the curly brackets, so {*.txt, *.csv} matches any file whose name ends with .txt or .csv, but not files which names end with '.pdf'
```

Data wrangling
```shell
grep # selects lines according to what they contain
wc # prints the number of characters, words, and lines in a file; you can make it print only one of those using -c, -w, or -l, respectively
sed # does pattern-matched string replacement
```

[Clone multiple repos from list](https://stackoverflow.com/questions/33649639/how-to-clone-a-list-of-git-repositories)
```shell
while read repo; do
    git clone "$repo"
done < projects.sh
```

Working with a remote server
```shell
scp -r D:/your_local_file_path your_username@your_IP_address:/your_remote_server_path # move data to a remote server
ping # check connection to remote address
htop # see which ports are being used in server
screen # keep server running
```

# Anaconda/ Conda snippets
[Working with Anaconda in Visual Studio Code](https://stackoverflow.com/questions/54828713/working-with-anaconda-in-visual-studio-code)
```json
"terminal.integrated.shellArgs.windows": [
       "PowerShell -NoExit -File C:\\ProgramFiles\\Anaconda\\shell\\condabin\\conda-hook.ps1"
    ]
```

[How to change the Jupyter start-up folder in your device](https://stackoverflow.com/questions/35254852/how-to-change-the-jupyter-start-up-folder) 
1. Run ```jupyter server --generate-config``` in ```cmd``` (or Anaconda Prompt)
2. Navigate to ```C:\Users\username\.jupyter\jupyter_notebook_config.py``` 
3. Replace ```#c.ServerApp.root_dir = ''``` with ```c.ServerApp.root_dir = '/the/path/to/desired/folder/'```

Basic environment setup
```conda
conda create --name "env_name" jupyterlab pandas seaborn scikit-learn # create environment and install main libraries
conda config --add channels conda-forge # add conda-forge channel
conda activate "env_name"
conda deactivate # deactivate environment
conda rename -n old_name -d new_name  # rename environment
```
[Rename environment](https://stackoverflow.com/questions/42231764/how-can-i-rename-a-conda-environment)
```conda
conda rename -n old_name -d new_name
```
[Clone conda environment](https://iq.opengenus.org/clone-conda-environment/)
```conda
conda create --name cloned_env --clone original_env
```conda

Kernel management and link to Jupyter
```shell
conda install nb_conda_kernels
conda install -c anaconda ipykernel # package to link Jupyter to Conda environments
ipython kernel install --user --name="name to show on Jupyter" # link Conda environment to Jupyter
```

Manage Jupyter kernels
```shell
jupyter kernelspec list 
jupyter kernelspec uninstall 'your_kernel_name'
```

Manage Jupyter Notebook sessions
```shell
jupyter notebook list 
jupyter notebook close 'your_port_number'
```

Package management
```shell
conda list -n 'environment_name' 'package name' # check if a specific package is installed and upgrade it
conda upgrade 'package_name' # upgrade package
conda 'package_name' = 'version_number' # install package in specific version
conda remove 'package_name'
```

Machine learning libraries
``` shell
conda install -c conda-forge xgboost # Xgboost gradient boosting
conda install -c conda-forge catboost # Catboost gradient boosting 
conda install -c conda-forge tensorflow # neural networks (pydot needed for some plots in tensorflow) 
conda install -c conda-forge shap # interpreting ML models 
conda install -c conda-forge spacy # text analysis 
conda install nltk # text analysis 
pip install aequitas # bias and fairness Audit Toolkit 
conda install -c districtdatalabs yellowbrick # machine learning visualization 
```


# Windows command prompt snippets
```shell
/? # get help
cls # clear screen
dir *.png # change directory
rename "hello.txt" "goodbye.txt"
mkdir parent\child
rmdir /s child
del # dele file
move
copy
xcopy # recursively copy a directory tree
tree # recursive directory listing
echo "some text" > filename.txt # add text to exis
echo "add some text" >> filename.txt
ipconfig # get address of local machine
wmic logicaldisk get name # obtain a list of drives
attrib # displays, sets, or removes attributes assigned to files or directories
dir > directory_tree.txt # print the current directory tree to a text file
set # prints a list of all environment variables
```
