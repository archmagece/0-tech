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
