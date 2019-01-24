# bash

## readfile


#while IFS='' read -r line || [[ -n "$line" ]]; do
#  echo "Text : $line"
#  if [[ $1 == "--exclude" ]];
#  then
#    echo $1
#done < "$CONFIG_FILE"


#command=''
#while IFS='' read -r line; do
#  echo $line
#  case "$line" in
#    \[rsync_includes\]) command="$command --include $line";;
#    \[rsync_excludes\]) command="$command --exclude $line";;
#    \[*) command= $command;;
#    *)  [ "$command"  -a "$line" ] && echo "$command $line"
#  esac
#done < $CONFIG_FILE
#echo "$command"


printSection()
{
  section_name="$1"
  found=false
  RSYNC_ARGS=''
  while read line
  do
    [[ $found == false && "$line" != "[$section_name]" ]] &&  continue
    # ignore empty
    [[ $found == true && "$line" =~ ^[\s\r\n]*$ ]] && continue
    # ignore comment
    [[ $found == true && "${line:0:1}" = '#' ]] && continue
    # break next section
    [[ $found == true && "${line:0:1}" = '[' ]] && break
    # skip first line - seciton name
    if [[ $found == false ]]
    then
      found=true
      continue
    fi
    RSYNC_ARGS="$RSYNC_ARGS --$section_name $line"
    # echo "$line"
  done < $CONFIG_FILE
  echo $RSYNC_ARGS
}
