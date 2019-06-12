# Bash CheatSheet

## comparison

https://www.tldp.org/LDP/abs/html/comparison-ops.html


a equals b
if [ "$s1" == "$s2" ]
if [[ "$s1" == "$s2" ]]
if [[ "$s1" -eq "$s2" ]]
a contains b
if [[ "$s1" == "$s2" ]]
bad space
if ["$s1" == "$s2"]
if [ "$s1" == "$s2" ]

## argument

한개씩 받기
$1 $2 $3

목록으로 받기
$@

for ARGS in "$@"
do
  ### aciton
fond

flag로 받기
https://www.tldp.org/LDP/abs/html/internal.html#EX33



for file in "$path"/*; do
    [ -f "$file" ] || continue
    mv "$file" "${file%.*}"
done

uname -s
uname -a

OS판별

http://woowabros.github.io/tools/2017/08/17/ost_bash.html

unameOut="$(uname -s)"
case "${unameOut}" in
    Linux*)     machine=Linux;;
    Darwin*)    machine=Mac;;
    CYGWIN*)    machine=Cygwin;;
    MINGW*)     machine=MinGw;;
    *)          machine="UNKNOWN:${unameOut}"
esac
echo ${machine}


bash file option - to 0-tech

-b filename - Block special file
-c filename - Special character file
-d directoryname - Check for directory Existence
-e filename - Check for file existence, regardless of type (node, directory, socket, etc.)
-f filename - Check for regular file existence not a directory
-G filename - Check if file exists and is owned by effective group ID
-G filename set-group-id - True if file exists and is set-group-id
-k filename - Sticky bit
-L filename - Symbolic link
-O filename - True if file exists and is owned by the effective user id
-r filename - Check if file is a readable
-S filename - Check if file is socket
-s filename - Check if file is nonzero size
-u filename - Check if file set-user-id bit is set
-w filename - Check if file is writable
-x filename - Check if file is executable

## directory list

```bash
for entry in "dir_name"/*
do
  echo $entry
  echo $(basename "$entry")
done
```