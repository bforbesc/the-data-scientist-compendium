# 🐚 shell


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
