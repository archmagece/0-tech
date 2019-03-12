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


