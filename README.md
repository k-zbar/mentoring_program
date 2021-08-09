# Mentoring_program

## Bash tasks
***
### Exercise 1 - Display Environment Variables
Create a script that, when run, will display the following environment variables to the console:
- USER
- HOME
- HISTCONTROL
- TERM
~~~
#!/bin/bash
clear
echo "This script will give us environment information"
echo "================================================"
echo ""
echo "Hello Username: $USER"
echo ""
echo "Your Home Directory is: $HOME"
echo ""
echo "Your History File Will Ignore: $HISTCONTROL"
echo ""
echo "Your Terminal Session Type is: $TERM"
echo ""
~~~
***
### Exercise 2 - Setting and Using Variables in Scripts
Write a script that sets FOUR variables:
- MYUSERNAME
- MYPASSWORD
- STARTOFSCRIPT
- ENDOFSCRIPT
~~~
#!/bin/bash
MYUSERNAME="username"
MYPASSWORD="password123"
STARTOFSCRIPT=`date`
echo "My login name for this application is: $MYUSERNAME"
echo "My login password for this application is: $MYPASSWORD"
echo "I started this script at: $STARTOFSCRIPT"
ENDOFSCRIPT=`date`
echo "I ended this script at: $ENDOFSCRIPT"
~~~
***
### Exercise 3 - Using Comments
Develop a script that creates, sets and displays two variables to the terminal when run. Within this script, add comments to explain what the script is doing, what each variable is and, using inline comments, what each command is doing.
~~~
#!/bin/bash
# This line is intended to be used as a general description of the script
# and anything that it does
clear    # clears the screen
# MYUSERNAME="Terry"    # the username for this application
MYUSERNAME="Don" # new username added later
echo "We are using the default user called: $MYUSERNAME" # display to the console
DATETIMESTAMP=`date`
echo "This is when the script was run: $DATETIMESTAMP" # this is the timestamp of run
~~~
***
### Exercise 4 - Using /dev/null
Create a simple script that does the following:
- Echo a full sentence to the terminal
- Echo a different full sentence, but redirect it to /dev/null<br/>
Run and display the results and make sure the statements appear where intended.
~~~
#!/bin/bash
# redirect to /dev/null example
echo "This is displaying on the console"
echo "This is going into the black hole" >> /dev/null
~~~
***
### Exercise 5 - Exit Status Types
Write a script that runs three commands:
- Evaluate an arithmetic expression
- Attempt to remove a file that does not exist in the current directory
- Evaluate another arithmetic expression<br/>
Immediately after each command, echo the exit status of that command to the terminal using the appropriate variable to show success and failure exit codes.
~~~ 
#!/bin/bash
# this is to show exit status types
set -e
expr 1 + 5
echo $?
rm doodles.sh
echo $?
expr 10 + 10
echo $?
~~~
***
### Exercise 6 - Evaluating Arithmetic Expressions
Write a script that evaluates and displays the following arithmetic operations:
- Add two numbers
- Add two numbers and multiply by a third, do not group anything 
- Add two numbers, grouped (changing order of precedence) and multiply by a third<br/>
Keep in mind special characters and/or escape characters as needed.
~~~
#!/bin/bash
# expression evaluation
expr 2 + 2
expr 2 + 2 \* 4
expr \( 2 + 2 \) \* 4
~~~
***
### Exercise 7 - Command Substitution
Write a script that will use command substitution to dynamically set variable values:
- TODAYSDATE - should contain date/time stamp when executed
- USERFILES - the results of a find run on the /home directory to list all files owned by 'user' account
***
Additionally, set two aliases:
- TODAY - should be an alias for the 'date' command
- UFILES - should be an alias to the full command used to set the variable USERFILES above<br/>
Finally, display all variables and alias values when the script is run. 
~~~
#!/bin/bash
# This script is intended to show how to do simple substitution
shopt -s expand_aliases
alias TODAY="date"
alias UFILES="find /home -user user"
TODAYSDATE=`date`
USERFILES=`find /home -user user`
echo "Today's Date: $TODAYSDATE"
echo "All Files Owned by USER: $USERFILES"
A=`TODAY`
B=`UFILES`
echo "With Alias, TODAY is: $A"
echo "With Alias, UFILES is: $B"
~~~
***
### Exercise 8 - Interactive Scripting
Create a script that interacts with the user. You will want to prompt the user to enter the following information (which you will capture and place into the following variables):
- FIRSTNAME
- LASTNAME
- USERAGE<br/>
Greet the user with their name and current age displayed and then calculate and display their age in 10 years.
~~~
#!/bin/bash
# interactive script for user input
echo "Enter Your First Name: "
read FIRSTNAME
echo "Enter Your Last Name: "
read LASTNAME
echo ""
echo "Your Full Name is: $FIRSTNAME $LASTNAME"
echo ""
echo "Enter Your Age: "
read USERAGE
echo "In 10 Years, You will be `expr $USERAGE + 10` years old."
~~~
***
### Exercise 9 - Using Arrays
Write a script intended to iterate through an array called SERVERLIST containing at least four values (server names). Display all four values to the terminal when run. 
~~~
#!/bin/bash
# simple array list and loop for display
SERVERLIST=("websrv01" "websrv02" "websrv03" "websrv04")
COUNT=0
for INDEX in ${SERVERLIST[@]}; do
  echo "Processing Server: ${SERVERLIST[COUNT]}"
  COUNT="`expr $COUNT + 1`"
done
~~~
***
### Exercise 10 - Passing Variables to Scripts at the Command Line
Create a script that, when run, will accept two command line values as arguments. These arguments should be a username and password and assigned to two variables in the script named appropriately. Finally, echo those values out to the terminal when run to indicate they were read and assigned as expected.
~~~
#!/bin/bash
# demo of command line values passed in with our shell script
USERNAME=$1
PASSWORD=$2
echo "The following Username is $USERNAME and Password is $PASSWORD"
~~~
***
### Exercise 11 - The If Statement
Create a script that interacts with the user. Prompt them to guess a secret number between 1 and 5. Read the guess from the terminal and assign it to a variable. Using the 'if' statement from the course, test that value to determine if they guessed the right number (you choose the correct value). If they do, display a success message, otherwise do nothing.
~~~
#!/bin/bash
# simple if script for guessing a number
echo "Guess the Secret Number"
echo "======================="
echo ""
echo "Enter a Number Between 1 and 5: "
read GUESS
if [ $GUESS -eq 3 ]
  then
    echo "You Guessed the Correct Number!"
fi
~~~
***
### Exercise 12 - Using If/Then/Else
Write a script that will prompt the user to enter a number between 1 and 3. Capture that number in a variable and then test that variable. Be sure to display the variable and it's value as appropriate within an if/then/else statement where the final statement will display if they did not enter a number between 1 and 3 telling them they failed to follow instructions. Redirect errors from each of the tests to /dev/null (to prevent script errors from showing if text is entered for example).
~~~
#!/bin/bash
# simple example of if then else and nested if statements
clear
echo "Enter a number between 1 and 3:"
read VALUE
if [ "$VALUE" -eq "1" ] 2>/dev/null; then
  echo "You entered #1"
elif [ "$VALUE" -eq "2" ] 2>/dev/null; then
  echo "You successfully entered #2"
elif [ "$VALUE" -eq "3" ] 2>/dev/null; then
  echo "You entered the 3rd number"
else
  echo "You didn't follow the directions!"
fi
~~~
***
### Exercise 13 - The For Statement
Write a script that assigns a variable that contains a list of all shell scripts (*.sh) in the current directory (command redirection). Using the 'for'statement from the course, iterate through that list of files and display the filename of each and cat out the contents to the terminal. 
~~~
#!/bin/bash
# this is a demo of the for loop
echo "List all the shell scripts contents of the directory"
SHELLSCRIPTS=`ls *.sh`
for SCRIPT in $SHELLSCRIPTS; do
  DISPLAY="`cat $SCRIPT`"
  echo "File: $SCRIPT - Contents $DISPLAY"
done
~~~
***
### Exercise 14 - Using the Case Statement
Develop a simple three item menu to display on the terminal. Your script, upon display of the menu, should prompt the user to choose one of the three available options. Using the 'case' statement from the course, display three unique messages depending on which number they chose, with a catch all message letting them know if they went outside the bounds of instructions.
~~~
#!/bin/bash
# demo of the case statement
clear
echo "MAIN MENU"
echo "========="
echo "1) Choice One"
echo "2) Choice Two"
echo "3) Choice Three"
echo ""
echo "Enter Choice: "
read MENUCHOICE

case $MENUCHOICE in
  1)
    echo "Congratulations for Choosing the First Option";;
  2)
    echo "Choice 2 Chosen";;
  3) 
    echo "Last Choice Made";;
  *)
    echo "You chose unwisely";;
esac
~~~
***
### Exercise 15 - While Looping
Create a script that prompts the user for a number. That number is to be used to display a simple message to the terminal X number of times (where X is the number captured from the user input). The message should include an indication of the number for each count the message is displayed. 
~~~
#!/bin/bash
# while loop example
echo "Enter the number of times to display the 'Hello World' message"
read DISPLAYNUMBER
COUNT=1
while [ $COUNT -le $DISPLAYNUMBER ]
do
  echo "Hello World - $COUNT"
  COUNT="`expr $COUNT + 1`"
done
~~~
***
### Exercise 16 - Reading Files
Create a simple text file containing a list of super heros (or some names if preferred), use at least four values, one per line in the file. Write a bash shell script that then reads that file and displays it line by line on the terminal window. 
~~~
#!/bin/bash
# simple file reading (non-binary) and displaying one line at a time
echo "Enter a filename to read: "
read FILE
while read -r SUPERHERO; do
  echo "Superhero Name: $SUPERHERO"
done < "$FILE"
~~~
***
### Exercise 17 - File Descriptors and Handles
Create a simple text file containing a list of names (superheroes) and name it whatever you wish, should contain at least four values, one per line. Write a script that will use a file descriptor defined for both reading and writing to that file (pick an appropriate number greater than the system reserved handles as talked about in the course). Filtering that file into an appropriate loop, display all values with that file. Finally, once complete, write a message with the time/date stamp to the file and close the descriptor.
~~~
#!/bin/bash
# demo of reading and writing to a file using a file descriptor
echo "Enter a file name to read: "
read FILE
exec 5<>$FILE

while read -r SUPERHERO; do
  echo "Superhero Name: $SUPERHERO"
done <&5

echo "File Was Read On: `date`" >&5
exec 5>&-
~~~
***
### Exercise 18 - IFS and Delimiting
Create a simple text file at the command prompt. This file should contain three values - CPU, Memory and Disk space for an imaginary system, all on one line and delimited with a '|' character. Write a script to read that file and prompt the user for the delimiter value. Use that delimiter along with the IFS variable and read those delimited values into three appropriately named variables. Finally, display them with labels, one each per line. 
~~~
#!/bin/bash
# delimiter example using IFS

echo "Enter filename to parse: "
read FILE
echo "Enter the Delimiter: "
read DELIM
IFS="$DELIM"

while read -r CPU MEMORY DISK; do
  echo "CPU: $CPU"
  echo "Memory: $MEMORY"
  echo "Disk: $DISK"
done <"$FILE"
~~~
***
### Exercise 19 - Traps and Signals
We need to create a menu for our users. Display a menu containing three choices AND a choice to allow them to exit. Display that menu and prompt for a choice. Upon choosing the value, it should simply clear the screen and redisplay the menu (loop until the exit choice is given). HOWEVER, we need to be sure that the end user cannot use CTL-C, CTL-Z or a KILL command to terminate the application. Add a 'trap' in the script to capture those attempts and provide instructions on how to exit the script using the menu choice instead.
~~~
#!/bin/bash
# example of trapping events and limiting the shell stopping
clear
trap 'echo " - Please Press Q to Exit.."' SIGINT SIGTERM SIGTSTP

while [ "$CHOICE" != "Q" ] && [ "$CHOICE" != "q" ]; do
  echo "MAIN MENU"
  echo "========="
  echo "1) Choice One"
  echo "2) Choice Two"
  echo "3) Choice Three"
  echo "Q) Quit/Exit"
  echo ""
  read CHOICE
  clear
done
~~~
***
### Exercise 20 - Error Handling with Exit
Create a script that accepts a command line parameter intended to be the name of a directory. With the script, attempt to change to the indicated directory, be sure to redirect errors to /dev/null on the command as we will be providing our own messaging. Test the results of the command to change directories. If it was successful, indicate success and display the contents of the directory. If it was not successful, indicate we cannot change directories and exit to the terminal with a custom exit code (less than 200).
~~~
#!/bin/bash
# demo of using error handling with exit
echo "Change to a directory and list the contents"
DIRECTORY=$1
cd $DIRECTORY 2>/dev/null

if [ "$?" = "0" ]; then
  echo "We can change into the directory $DIRECTORY, and here are the contents"
  echo "`ls -al`"
else
  echo "Cannot change directories, exiting with an error and no listing"
  exit 111
fi
~~~
***
### Exercise 21 - Creating a Function
Create a simple script containing a single function. This function should display a message to clearly indicate it was generated when the function was run. Then, display another message outside the function clearly indicating it was generated outside of it.
~~~
vagrant@ubuntu-xenial:~/task22$ tree
.
├── file
└── sub1
    └── sub2
        └── s_link -> /home/vagrant/task22/file

2 directories, 2 files
~~~
~~~
vagrant@ubuntu-xenial:~/task22$ find ./ -type l -exec bash -c 'ln -snf $(realpath --relative-to=$(dirname "$0") $(readlink -f "$0")) "$0"' {} \;
vagrant@ubuntu-xenial:~/task22$ tree
.
├── file
└── sub1
    └── sub2
        └── s_link -> ../../file

2 directories, 2 files
~~~
***
### Exercise 22 - Variable Scope in Functions
Create a script to demonstrate the visibility of variables and when they are available within a script and its functions. Define a global variable, a function that defines a local variable and then display both BEFORE calling the function, call the function, then display both AFTER calling the function. 
~~~
#!/bin/bash
# demonstrating variable scope
# global variable declaration
GLOBALVAR="Globally Visible"

# function definitions - start
# sample function for function variable scope

funcExample () {
  # local variable to the function
  LOCALVAR="Locally Visible"
  echo "From within the function, the variable is $LOCALVAR..."
}

# functions definitions - stop
# script - start
clear
echo "This step happens first..."
echo ""
echo "GLOBAL variable = $GLOBALVAR (before the function call)"
echo "LOCALVAR variable = $LOCALVAR (before the function call)"
echo ""
echo "Calling Function - funcExample()"
echo ""
funcExample
echo ""
echo "Function has been called..."
echo ""
echo "GLOBAL variable = $GLOBALVAR (after the function call)"
echo "LOCALVAR variable = $LOCALVAR (after the function call)"
~~~
***
### Exercise 23 - Functions with Parameters
Write a script that takes a single command line parameter intended to be the user's first name. Prompt the user for their age and read that into a variable. Using the appropriate method to make that command line parameter visible to a function, pass the age captured to the function and display a message to the user addressing them by name and confirming their age, add a calculation of their age in number of days. 
~~~
#!/bin/bash
# this demo is for functional parameter passing
# global variable
USERNAME=$1
# function definitions - start

# calculate age in days
funcAgeInDays () {
  echo "Hello $USERNAME, You are $1 Years Old."
  echo "That makes you approximately `expr $1 \* 365` days old..."
}

# function definitions - stop
# scrip - start
clear
echo "Enter Your Age: "
read USERAGE

# calculate the number of days
funcAgeInDays $USERAGE
~~~
***
### Exercise 24 - Nested Functions
We are going to use nested functions to simulate the kind of abstraction you find in many object oriented languages. Create the following structures in your script:
- a function that defines two local variables to hole the number of arms and legs that a human being has
- nested functions, one for each a male and female, that contain the appropriate number of beards that each gender has
- capture the gender as a command line parameter
- test the command line parameter and call the appropriate functions in order to display the characteristics of the indicated gender
~~~
#!/bin/bash
# demo of nested functions and some abstraction
# global variable
GENDER=$1

# function definitions - start

# create a human being
funcHuman () {
  ARMS=2
  LEGS=2
  echo "A Human has $ARMS arms and $LEGS legs - but what gender are we?"
  echo ""

  funcMale () {
    BEARD=1
    echo "This man has $ARMS arms and $LEGS legs, with $BEARD beard(s)..."
    echo ""
  }
  funcFemale () {
    BEARD=0
    echo "This woman has $ARMS arms and $LEGS legs, with $BEARD beard(s)..."
    echo ""
  }
}

# function definitions - stop

# script - start
clear
echo "Determining the characteristics of the gender $GENDER"
echo ""

# determine the actual gender and display the characteristics
if [ "$GENDER" == "male" ]; then
  funcHuman
  funcMale
else
  funcHuman
  funcFemale
fi
~~~
***
### Exercise 25 - Simple Infobox
We want to display a simple Information Box for our end users prior to executing a command. Accept one command line parameter when executing the script. This box should use the dialog control as shown in the course and display for a total of 5 seconds. The title and message in the box should be passed into the function but can be whatever you like that will warn the user if the parameter passed in was 'shutdown', otherwise an innocuous message can be displayed.
~~~
#!/bin/bash
# demo of a simple info box with dialog and ncurses

# global variables / default values
INFOBOX=${INFOBOX=dialog}
TITLE="Default"
MESSAGE="Something to say"
XCOORD=10
YCOORD=20

# function declarations - start
# display the infobox and our mesage
funcDisplayInfoBox () {
  $INFOBOX --title "$1" --infobox "$2" "$3" "$4"
  sleep "$5"
}

# function declarations - stop
# script - start

if [ "$1" == "shutdown" ]; then
  funcDisplayInfoBox "WARNING!" "We are SHUTTING DOWN the System..." "11" "21" "5"
  echo "Shutting Down!"
else
  funcDisplayInfoBox "Information..." "You are not doing anything fun..." "11" "21" "5"
  echo "Not doing anything..."
fi

# script - stop
~~~
***
### Exercise 26 - Displaying a Message Box
We want to display a simple Message Box for our end users prior to executing a command. Accept one command line parameter when executing the script. This box should use the dialog control as shown in the course and display until the OK button is clicked or selected. The title and message in the box should be passed into the function but can be whatever you like that will warn the user if the parameter passed in was 'shutdown', otherwise an innocuous message can be displayed. 
~~~
#!/bin/bash
# demo of a message box with an OK button

# global variables / default variables
MSGBOX=${MSGBOX=dialog}
TITLE="Default"
MESSAGE="Some Message"
XCOORD=10
YCOORD=20

# function declarations - start

# display the message box with our message
funcDisplayMsgBox () {
  $MSGBOX --title "$1" --msgbox "$2" "$3" "$4"
}

# function declarations - stop

# script - start
if [ "$1" == "shutdown" ]; then
  funcDisplayMsgBox "WARNING!" "Please press OK when you are ready to shut down the system" "10" "20"
  echo "SHUTTING DOWN NOW!!!"
else
  funcDisplayMsgBox "Boring..." "You are not asking for anything fun..." "10" "20"
  echo "Not doing anything, back to regular scripting..."
fi

# script - stop
~~~
***
### Exercise 27 - A User Input Box
In this script, we will be using an Input Box constructed from the dialog control, to prompt the user for a filename to display to the terminal. Construct the input box within a function and capture the value input using the appropriate output method to a file. Read that file back in and attempt to display (cat) the file to the terminal or indicate that it does not exist.
~~~
#!/bin/bash
# simple demo of an input dialog box

# global variables / default values
INPUTBOX=${INPUTBOX=dialog}
TITLE="Default"
MESSAGE="Something to display"
XCOORD=10
YCOORD=20

# function declarations - start

# display the input box
funcDisplayInputBox () {
  $INPUTBOX --title "$1" --inputbox "$2" "$3" "$4" 2>tmpfile.txt
}

# function declarations - stop
# script - start
funcDisplayInputBox "Display File Name" "Which file in the current directory do you want to display?" "10" "20"

if [ "`cat tmpfile.txt`" != "" ]; then
  cat "`cat tmpfile.txt`"
else
  echo "Nothing to do"
fi
 
# script - stop
~~~
***
### Exercise 28 - Creating a Menu
Using the dialog control from the course, develop a function inside a script that will display a menu containing at least four choices. Capture the indicated value using hte appropriate output to a file. Reading that file, test the value and display an appropriate message, different for each on.
~~~
#!/bin/bash
# demo of a dialog box that will display a menu

# global variables / default values
MENUBOX=${MENUBOX=dialog}

# function declarations - start

# function to display a simple menu
funcDisplayDialogMenu () {
  $MENUBOX --title "[ M A I N   M E N U ]" --menu "Use UP/DOWN Arrows to Move and Select or the Number of Your Choice and Enter" 15 45 4 1 "Display Hello World" 2 "Display Goodbye World" 3 "Display Nothing" X "Exit" 2>choice.txt
}

# function declarations - stop

# script - start
funcDisplayDialogMenu

case "`cat choice.txt`" in
  1) echo "Hello World";;
  2) echo "Goodbye World";;
  3) echo "Nothing";;
  X) echo "Exit";;
esac

# script - stop
~~~
***
### Exercise 29 - 
Вывести всех пользователей которые (имеют/не имеют) терминала (bash, sh, zsh and etc.) (две команды).
~~~

~~~
***
### Exercise 30 - 
Со страницы из интернета закачать все ссылки, которые на странице. Закачивать параллельно. Использовать curl и wget. Дать рекомендации по использованию.
curl
~~~

~~~
***
### Exercise 31 - 
Остановить процессы, которые работают больше 5 дней. Команду ps не использовать.
~~~

~~~
***
### Exercise 32 - 
Имется дериктория, в которой, существуют папки и файлы (\*.txt & \*.jpeg). Файлы \*.txt и \*.jpeg однозначно связаны между собой по префиксу имени. Файлы могут находиться в различном месте данной директории. Нужно удалить все \*.jpeg для которых не существует файла \*.txt.
~~~

~~~
***
### Exercise 33 - 
Find your IP address using the command line.
~~~

~~~
***
### Exercise 34 - 
Получить все ip-адресса из текстового файла.
~~~

~~~
***
### Exercise 35 - 
Найти все активные хосты использую/не используя nMAP в: 
- заданной сети 
~~~

~~~
***
### Exercise 36 - 
Получить все поддомены из SSL сертификата.
~~~

~~~