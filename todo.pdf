#!/bin/bash

#function to work out what the user wants to change and change it on their desired line
alter () {
	#change priority
        if [[ $priority != "N.A" ]]

      	then
                replace=$(sed -n "${modify}p" ${list} | awk -v col=7 '{print $col}')
                sed "${modify}s/${replace}/${priority}/" $list > temp && mv temp $list

        fi
	#change due date
        if [[ $due != "N.A" ]]

        then
                replace=$(sed -n "${modify}p" ${list} | awk -v col=5 '{print $col}')

                sed "${modify}s/${replace}/${due}/" $list > temp && mv temp $list

        fi
	#change tags 
        if [[ $tags != "N.A" ]]

        then

                replace=$(sed -n "${modify}p" ${list} | awk -v col=9 '{print $col}')

                sed "${modify}s/${replace}/${tags}/" $list > temp && mv temp $list

        fi

}

#function to change the progress of the desired task to complete
completed () {

        replace=$(sed -n "${complete}p" ${list} | awk -v col=11 '{print $col}')

        sed "${complete}s/${replace}/completed/" $list > temp && mv temp $list

	reccurence=$(sed -n "${modify}p" ${list} | awk -v col=13 '{print $col}')

	newtask=

	if [[ $reccurence = "weekly" ]]
	then

	fi

 }

#function to delete the desired task
deleting () {

        sed -e "${delete}d" $list > temp && mv temp $list

}

#function to input the task inputted by the user into the desired list
inputTask () {

	#work out new id
        last=$(tail -1 $list)
        id=${last:0:1}
        id=$((id+1))

	#input
        echo "$id | $task | $due | $priority | $tags | $progress | $recurring " >> $list

}

#display list sorting by users choice of priority
prioritysort () {

        while IFS= read -r line

        do

        word=$(echo $line | awk '{print $7}')

                if [[ $word == $sortPriority ]]

                then

                     echo $line | awk '{print $0}'

                fi

        done < $list

}

#sort list by users choice of tag
tagSort () {

        while IFS= read -r line

        do

                word=$(echo $line | awk '{print $9}')

                if [[ $word == $sortTags ]]

                then

                        echo $line | awk '{print $0}'

                fi

        done < $list
}

#sort by users choice of due date
dueSort () {

        while IFS= read -r line

        do

                IFS=- read -r var1 var2 var3 <<< line

		echo $var2

                if [[ $word == $var2 ]]

                then

                        echo $line | awk '{print $0}'

                fi

        done < $list

}

#search for tags inputted by user and display matching results
search () {

        while IFS= read -r line

        do

                word=$(echo $line | awk '{print $9}')

                if [[ $word == $tagSearch ]]

                then

                        echo $line | awk '{print $0}'

                fi

        done < $list

}

#set up variables
list=""

task="N.A"

due="YYYY-MM-DD"

priority="N.A"

progress=incomplete

tags="N.A"

modify=""

delete=""

complete=""

recurring="N.A"

sortDue=""

sortPriority=""

sortTags=""

tagSearch=""

#loop through inputed values and chnage variables depending on the input by the user
while [[ $# -gt 0 ]]

do
	#case to do so
        case "$1" in

                --list)
                list=$2
                shift 2
                ;;
                --task)
                task=$2
                shift 2
                ;;
                --due)
                due=$2
                shift 2
                ;;
                --priority)
                priority=$2
                shift 2
                ;;
                --tags)
                tags=$2
                shift 2
                ;;
                --progress)
                progress=$2
                shift 2
                ;;
                --delete)
                delete=$2
                shift 2
                ;;
                --modify)
                modify=$2
                shift 2
                ;;
                --complete)
                complete=$2
		shift 2
                ;;
                --recurring)
                recurring=$2
		shift 2
                ;;
                --sortDue)
                sortDue=$2
		shift 2
                ;;
                --sortPriority)
                sortPriority=$2
		shift 2
                ;;
                --sortTags)
                sortTags=$2
		shift 2
                ;;
		--tagSearch)
		tagSearch=$2
		shift 2
		;;
        esac
done

#make sure user has inputted a list
if [[ $list == "" ]]

then

        echo error list must be included

fi

#check if user wants to modify something and call fucntion to do so
if [[ $modify != "" ]]

then
        alter

fi

#check if user wanted to set a task as complete 
if [[ $complete != "" ]]

then

        completed

fi

#check if user wants to delete a task
if [[ $delete != "" ]]

then
        deleting

fi

#check if user wants to input a task
if [[ $task != "N.A" ]]

then

        inputTask

fi

#check if user wants to display list by priority
if [[ $sortPriority != "" ]]

then
    prioritysort

fi

#check if user wants to display by tags
if [[ $sortTags != "" ]]

then

       tagSort

fi

#check if user wants to display by due
if [[ $sortDue != "" ]]

then

        dueSort

fi

#check if user wants to seach for tag 
if [[ $tagSearch != "" ]]

then

        search

fi
