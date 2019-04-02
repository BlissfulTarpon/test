# BASH

The Bourne Again Shell. Extension of the previous SH shell.

## INTRO

sh - shell (old)

.sh = Shell script file executable.


## REDIRECTION

| OPERATOR    | DESC                          |
|-------------|-------------------------------|
| >           | Redirect STDOUT to file       |
| <           | Input from file               |
| 2>          | Redirect STDERR to file       |
| 2>/dev/null | Suppress STDERR               |
| &>          | Redirect all output to a file |
| >>          | Append instead of overwrite   |
|             |                               |

## BASIC STRUCTURE

		#!/bin/bash

			while:
				do
					date
					sleep 5
				done

With if statements

    if [statement is true]; then
        do this thing
    else
        do this other thing
    fi


## MISC

To use special characters in a command, use the ''

    mkdir '#trending'

Backslash (\) are used to escape next character.

    mkdir \*special\! # would create the folder -star-special!

Single quotes are used to pass the text inside as is. Double quotes expands values inside to their meaning.

Default prompt is PS1. To check your current prompt:

    echo $PS1

IFS is used to format the returned output (used in scripts)

    IFS=,

Ampersands are used to manage processes. && at the end of a command will only execute what is after if the previous command exited successfully (0).

    yum update && shutdown now

To execute multiple commands, use the curly brackets {}

    yum update && {ping google.com ; shutdown now}

## ENVIRONMENT VARIABLES

These are used to store values. Erased upon exiting or when opening a new shell. Use "export" to save system-wide.

    new_variable="long name in quotes" # sets the variable
    unset new_variable # remove the variable
    $new_variable # call a variable with the dollar sign
    echo $new_variable # to check the content of a variable
    export MYDIR=/usr/mydir # Creates env. variable "MYDIR" working across the entire system


Some built-in variables

HISTCONTROL=ignoredups # ignores duplicates in history
HISTCONTROL=ignoredups:ignorespace # use : to separate if you want to pass more than one value

## FUNCTIONS

Functions are long line of codes stored in memory. Similar to scripts but not stored in a file.

    function name_function() {
        code you -n | want to execute
    }

Then simply call the function by its name.

    unset -f name_function # to remove
    declare -f name_function # to check content

## POSITIONAL VARIABLES

-dollarsign-1 -dollarsign-2 $n are input user make.
-dollarsign-0 calls the name of the script
-dollarsign-* and -dollarsign-@ prints all the variables

Consider the following script:

    echo -dollarsign-1 -dollarsign-2

And running the script like this

    ./script.sh Jake Jenny

Would return

    Jake Jenny

You can use variables as command or file input

    var=$(command)
    var=$(<text.txt)

When using an argument, use the following to have a default value instead of breaking the script.

    firstname=$1
    echo ${firstname:- # default value you want}
                    :? # Display message
                    :2 # slice output starting at 2nd character
                    :2:4 # slice for only 4 character after

When using the $1 in scripts, they refer to arguments passed from the CLI at the time they ran the script

    ./script.sh argument1.txt 3

In the case above, "argument1.txt" is $1 and the "3" is the -dollarsign-2. Note that -dollarsign-0 is always referring to the script name.

## LOOPS

    if condition; then
        code
    elif condition
        code
    else
        code
    fi

## WHILE / UNTIL LOOPS

Same syntax, while runs as long as True, until runs as long as False.

## FOR LOOPS

    for phrase in "me" "myself" "I"; do
        echo $phrase
    done

The following would run the script as long as i is smaller than 10. It increments +1 everytime it runs.

    for ((i=10 ; i>10 ; i++)); do
        echo $i
    done

## CASE LOOPS

    case $order
        in
            x-h
                echo "blabla" ;;
    esac

## SELECT STATEMENTS

    select variable
        [in
        set
        ]
    do
        code
    done

Use $REPLY for stored value
Break;; will terminate the shell

## TESTING CONDITIONS

Double square brackets [[ allow for expansions

    -n # string is not null
    -z # string is null
    -a # file exists
    -s # file exists and is not empty

Testing for integers

    -lt # lower than
    -gt # greater than
    -eq # equal
    -ne # not equal
    -ge # greater or equal

    -double square brackets- 0 -lt 2 -double square brackets- && echo "Yes"

## SHIFT

The shift command pushes the argument one tick forward.

    opt=$1
    arg1=$2
    arg2=$3

      if [ $1 = -1]; then
          shift
      fi

## DECLARE

To convert to integer use

    declare -i result=5*4
  > 20

## ARRAYS

Hold multiple values inside a variable

shells[0]=bash
shells[1]=fish
shells[2]=zsh
OR
shells=(bash fish zsh)

To retrieve elements use

    echo ${shells[0]} # print the first value
    echo ${shells[*]} # print all the values. Use IFS to change the output format
    echo ${!shells[@]} # print all available values

## READ

Enters multiple values without prompts

    read variable1 variable2
  > John Doe
    print $variable1
  > John

To read a full array

    read -a
