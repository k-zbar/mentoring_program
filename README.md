# Mentoring_program

## Bash tasks
***
### Exercise 1
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
### Exercise 2
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
### Exercise 3
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
### Exercise 4
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
### Exercise 5
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
### Exercise 6
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
### Exercise 7
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
### Exercise 8
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
### Exercise 9
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
### Exercise 10
Create a script that, when run, will accept two command line values as arguments. These arguments should be a username and password and assigned to two variables in the script named appropriately. Finally, echo those values out to the terminal when run to indicate they were read and assigned as expected.
~~~
#!/bin/bash
# demo of command line values passed in with our shell script
USERNAME=$1
PASSWORD=$2
echo "The following Username is $USERNAME and Password is $PASSWORD"
~~~
***
### Exercise 11
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
### Exercise 12
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
### Exercise 13
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
### Exercise 14
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
### Exercise 15
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
### Exercise 16
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
### Exercise 17
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
### Exercise 18
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
### Exercise 19
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
### Exercise 20
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
### Exercise 21
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
### Exercise 23
23) В указанной директории найти все сломанные ссылки и удалить их. 
~~~
vagrant@ubuntu-xenial:~/links$ ll
total 8
drwxrwxr-x 2 vagrant vagrant 4096 Feb 15 18:22 ./
drwxr-xr-x 6 vagrant vagrant 4096 Feb 15 18:15 ../
lrwxrwxrwx 1 vagrant vagrant   13 Feb 15 18:22 brake_link_1 -> no_exist_file
lrwxrwxrwx 1 vagrant vagrant   13 Feb 15 18:22 brake_link_2 -> no_exist_file
lrwxrwxrwx 1 vagrant vagrant   13 Feb 15 18:22 brake_link_3 -> no_exist_file
-rw-rw-r-- 1 vagrant vagrant    0 Feb 15 18:22 file
lrwxrwxrwx 1 vagrant vagrant    4 Feb 15 18:22 good_link -> file
~~~
~~~
vagrant@ubuntu-xenial:~/links$ find . -xtype l -delete
vagrant@ubuntu-xenial:~/links$ ll
total 8
drwxrwxr-x 2 vagrant vagrant 4096 Feb 15 18:22 ./
drwxr-xr-x 6 vagrant vagrant 4096 Feb 15 18:15 ../
-rw-rw-r-- 1 vagrant vagrant    0 Feb 15 18:22 file
lrwxrwxrwx 1 vagrant vagrant    4 Feb 15 18:22 good_link -> file
~~~
***
### Exercise 24
24) Распаковать из архива tar, gz, bz2, lz, lzma, xz, Z определенный каталог в указанное место. 
~~~
vagrant@ubuntu-xenial:~/archives$ ll
total 40
drwxrwxr-x  2 root root  4096 Feb 13 14:37 ./
drwxr-xr-x 10 root root  4096 Feb 13 14:10 ../
-rw-rw-r--  1 root root  6276 Feb 13 14:55 file.Z
-rw-rw-r--  1 root root    14 Feb 13 14:23 bzip2.bz2
-rw-rw-r--  1 root root    23 Feb 13 14:22 gz.gz
-rw-rw-r--  1 root root    36 Feb 13 14:25 lz.lz
-rw-rw-r--  1 root root    18 Feb 13 14:26 lzma.lzma
-rw-rw-r--  1 root root 10240 Feb 13 14:13 tar.tar
-rw-rw-r--  1 root root    32 Feb 13 14:27 xz.xz
~~~
~~~
vagrant@ubuntu-xenial:~/archives$ tar -xvf tar.tar
vagrant@ubuntu-xenial:~/archives$ gunzip gz.gz
vagrant@ubuntu-xenial:~/archives$ bzip2 -d bzip2.bz2
vagrant@ubuntu-xenial:~/archives$ lzip -d lz.lz
vagrant@ubuntu-xenial:~/archives$ lzma -d lzma.lzma
vagrant@ubuntu-xenial:~/archives$ unxz xz.xz
vagrant@ubuntu-xenial:~/archives$ uncompress file.Z
~~~
tar
~~~
vagrant@ubuntu-xenial:~/archives$ tar -cvf tar.tar dir1 dir2
vagrant@ubuntu-xenial:~/archives$ tar -C /home/archives2 -xf tar.tar dir2
~~~
gz
~~~
vagrant@ubuntu-xenial:~/archives$ gzip tar.tar
vagrant@ubuntu-xenial:~/archives$ tar -C /home/archives2 -xf tar.tar.gz dir1
~~~
bz2
~~~
vagrant@ubuntu-xenial:~/archives$ bzip2 tar.tar
vagrant@ubuntu-xenial:~/archives$ tar -C /home/archives2 -xf tar.tar.bz2 dir1
~~~
lz
~~~
vagrant@ubuntu-xenial:~/archives$ lzip tar.tar
vagrant@ubuntu-xenial:~/archives$ tar -C /home/archives2 -xf tar.tar.lz dir1
~~~
lzma
~~~
vagrant@ubuntu-xenial:~/archives$ lzma tar.tar
vagrant@ubuntu-xenial:~/archives$ tar -C /home/archives2 -xf tar.tar.lzma dir2
~~~
xz
~~~
vagrant@ubuntu-xenial:~/archives$ xz tar.tar
vagrant@ubuntu-xenial:~/archives$ tar -C /home/archives2 -xf tar.tar.xz dir2
~~~
Z
~~~
vagrant@ubuntu-xenial:~/archives$ compress tar.tar
vagrant@ubuntu-xenial:~/archives$ tar -C /home/archives2 -xf tar.tar.Z dir2
~~~
***
### Exercise 25
25) Рекурсивно скопировать структуру каталогов из указанной директории (без файлов). 
~~~
vagrant@ubuntu-xenial:~$ tree dir1 destination
dir1
├── dir2
│   ├── dir3
│   │   └── file3
│   └── file2
└── file1
destination
~~~
~~~
vagrant@ubuntu-xenial:~$ rsync -av -f"+ */" -f"- *" "dir1" "destination"
sending incremental file list
dir1/
dir1/dir2/
dir1/dir2/dir3/

sent 134 bytes  received 28 bytes  324.00 bytes/sec
total size is 0  speedup is 0.00
vagrant@ubuntu-xenial:~$ tree dir1 destination
dir1
├── dir2
│   ├── dir3
│   │   └── file3
│   └── file2
└── file1
destination
└── dir1
    └── dir2
        └── dir3

5 directories, 3 files
~~~
~~~
vagrant@ubuntu-xenial:~/task25$ find folder1/ -type d -exec bash -c 'mkdir destination/{}' \;
vagrant@ubuntu-xenial:~/task25$ tree
.
├── destination
│   └── folder1
│       └── folder2
│           └── folder3
└── folder1
    ├── file1
    └── folder2
        ├── file2
        └── folder3
            └── file3

7 directories, 3 files
~~~
***
### Exercise 26
26) Вывести список всех пользователей системы (только имена) по алфавиту.
~~~
vagrant@ubuntu-xenial:~/task17$ cat /etc/passwd | cut -d: -f1 | sort
_apt
backup
bin
daemon
dnsmasq
games
gnats
irc
list
lp
lxd
mail
man
messagebus
news
nobody
pollinate
proxy
root
sshd
sync
sys
syslog
systemd-bus-proxy
systemd-network
systemd-resolve
systemd-timesync
ubuntu
uucp
uuidd
vagrant
www-data
~~~
***
### Exercise 27
27) Вывести список всех системных пользователей системы отсортированных по id, в формате: login id. 
~~~
vagrant@ubuntu-xenial:~/task17$ cat /etc/passwd | egrep "x:(0?[1-9]|[1-9][0-9]):" | cut -d: -f1,3 | tr -s ':' ' ' | sort -k 2n
daemon 1
bin 2
sys 3
sync 4
games 5
man 6
lp 7
mail 8
news 9
uucp 10
proxy 13
www-data 33
backup 34
list 38
irc 39
gnats 41
~~~
***
### Exercise 28
28) Вывести список всех пользователей системы (только имена) отсортированные по id.
~~~
vagrant@ubuntu-xenial:~$ cat /etc/passwd | egrep "x:(0?[1-9]|[1-9][0-9]):" | cut -d: -f1,3 | tr -s ':' ' ' | sort -k 2n | cut -d' ' -f1
daemon
bin
sys
sync
games
man
lp
mail
news
uucp
proxy
www-data
backup
list
irc
gnats
~~~
***
### Exercise 29
29) Вывести всех пользователей которые не имеют право авторизовываться или не имеют право авторизовываться в системе (две команды).
~~~
vagrant@ubuntu-xenial:~$ cat /etc/passwd | cut -d: -f1,7 | tr -s ':' ' ' | grep nologin
daemon /usr/sbin/nologin
bin /usr/sbin/nologin
sys /usr/sbin/nologin
games /usr/sbin/nologin
man /usr/sbin/nologin
lp /usr/sbin/nologin
mail /usr/sbin/nologin
news /usr/sbin/nologin
uucp /usr/sbin/nologin
proxy /usr/sbin/nologin
www-data /usr/sbin/nologin
backup /usr/sbin/nologin
list /usr/sbin/nologin
irc /usr/sbin/nologin
gnats /usr/sbin/nologin
nobody /usr/sbin/nologin
sshd /usr/sbin/nologin
~~~
~~~
vagrant@ubuntu-xenial:~$ cat /etc/passwd | cut -d: -f1,7 | tr -s ':' ' ' | grep -v nologin
root /bin/bash
sync /bin/sync
systemd-timesync /bin/false
systemd-network /bin/false
systemd-resolve /bin/false
systemd-bus-proxy /bin/false
syslog /bin/false
_apt /bin/false
lxd /bin/false
messagebus /bin/false
uuidd /bin/false
dnsmasq /bin/false
pollinate /bin/false
vagrant /bin/bash
ubuntu /bin/bash
~~~
***
### Exercise 30
30) Вывести всех пользователей которые (имеют/не имеют) терминала (bash, sh, zsh and etc.) (две команды).
~~~
vagrant@ubuntu-xenial:~$ cat /etc/passwd | cut -d: -f1,7 | tr -s ':' ' ' | grep bash | cut -d' ' -f1
root
vagrant
ubuntu
~~~
~~~
vagrant@ubuntu-xenial:~$ cat /etc/passwd | cut -d: -f1,7 | tr -s ':' ' ' | grep -v bash  | cut -d' ' -f1
daemon
bin
sys
sync
games
man
lp
mail
news
uucp
proxy
www-data
backup
list
irc
gnats
nobody
systemd-timesync
systemd-network
systemd-resolve
systemd-bus-proxy
syslog
_apt
lxd
messagebus
uuidd
dnsmasq
sshd
pollinate
~~~
***
### Exercise 31
31) Со страницы из интернета закачать все ссылки, которые на странице. Закачивать параллельно. Использовать curl и wget. Дать рекомендации по использованию.
curl
~~~
vagrant@ubuntu-xenial:~$ curl https://davidwalsh.name/scrape-images-wget | grep -Po "(http|https)://([\w_-]+(?:(?:\.[\w_-]+)+))([\w.,@?^=%&:/~+#-]*[\w@?^=%&/~+#-])?" | xargs -n 1 -P 2 -I{} wget {}
~~~
wget
~~~
vagrant@ubuntu-xenial:~$ wget -nd -r -P /home/vagrant/links/images -A jpeg,jpg,bmp,gif,png https://davidwalsh.name/scrape-images-wget
~~~
***
### Exercise 32
32) Остановить процессы, которые работают больше 5 дней. Команду ps не использовать.
~~~
vagrant@ubuntu-xenial:~$ ps -wo pid,etime
  PID     ELAPSED
 2194    04:01:12
21406       00:00

~~~
~~~
vagrant@ubuntu-xenial:~$ kill -9 $(find /proc -maxdepth 1 -user vagrant -type d -mmin +60 -exec basename {} \; | tail -n +3)
~~~
***
### Exercise 33
33) Имется дериктория, в которой, существуют папки и файлы (\*.txt & \*.jpeg). Файлы \*.txt и \*.jpeg однозначно связаны между собой по префиксу имени. Файлы могут находиться в различном месте данной директории. Нужно удалить все \*.jpeg для которых не существует файла \*.txt.
~~~
vagrant@ubuntu-xenial:~$ tree txt_jpeg
txt_jpeg
├── company_logo.jpeg
├── no_link.jpeg
├── sub_dir
│   └── company_bio.txt
├── user_bio.txt
└── user_photo.jpeg
~~~
~~~
vagrant@ubuntu-xenial:~/txt_jpeg$ rm -r $(find . -type f -exec basename {} \; | cut -d_ -f1 | sort | uniq -u)*
vagrant@ubuntu-xenial:~$ tree txt_jpeg
txt_jpeg
├── company_logo.jpeg
├── sub_dir
│   └── company_bio.txt
├── user_bio.txt
└── user_photo.jpeg
~~~
***
### Exercise 34
34) Find your IP address using the command line.
~~~
vagrant@ubuntu-xenial:~$ ip a | grep inet | cut -d' ' -f6 | grep -E -o "([0-9]{1,3}[\.]){3}[0-9]{1,3}"
127.0.0.1
10.0.2.15
10.23.104.28
~~~
***
### Exercise 35
35) Получить все ip-адресса из текстового файла.
~~~
vagrant@ubuntu-xenial:~$ touch ip_list.txt
vagrant@ubuntu-xenial:~$ nano ip_list.txt
vagrant@ubuntu-xenial:~$ cat ip_list.txt
This file has lots of IP addresses:
1. Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : kyiv.epam.com
   Link-local IPv6 Address . . . . . : fe80::2d9c:3c28:430e:e7af%15
   IPv4 Address. . . . . . . . . . . : 10.23.106.15

2. Ethernet adapter Ethernet1:

   Connection-specific DNS Suffix  . : kyiv.epam.com
   Link-local IPv6 Address . . . . . : fe80::2d9c:3c28:430e:e7af%15
   IPv4 Address. . . . . . . . . . . : 33.119.205.147

3. Ethernet adapter Ethernet2:

   Connection-specific DNS Suffix  . : kyiv.epam.com
   Link-local IPv6 Address . . . . . : fe80::2d9c:3c28:430e:e7af%15
   IPv4 Address. . . . . . . . . . . : 105.52.219.79

4. Ethernet adapter Ethernet3:

   Connection-specific DNS Suffix  . : kyiv.epam.com
   Link-local IPv6 Address . . . . . : fe80::2d9c:3c28:430e:e7af%15
   IPv4 Address. . . . . . . . . . . : 53.89.250.195

5. Ethernet adapter Ethernet4:

   Connection-specific DNS Suffix  . : kyiv.epam.com
   Link-local IPv6 Address . . . . . : fe80::2d9c:3c28:430e:e7af%15
   IPv4 Address. . . . . . . . . . . : 150.216.144.82

6. Ethernet adapter Ethernet5:

   Connection-specific DNS Suffix  . : kyiv.epam.com
   Link-local IPv6 Address . . . . . : fe80::2d9c:3c28:430e:e7af%15
   IPv4 Address. . . . . . . . . . . : 241.25.212.52

7. Ethernet adapter Ethernet6:

   Connection-specific DNS Suffix  . : kyiv.epam.com
   Link-local IPv6 Address . . . . . : fe80::2d9c:3c28:430e:e7af%15
   IPv4 Address. . . . . . . . . . . : 187.150.175.127
~~~
~~~
vagrant@ubuntu-xenial:~$ grep -E -o "([0-9]{1,3}[\.]){3}[0-9]{1,3}" ip_list.txt
10.23.106.15
33.119.205.147
105.52.219.79
53.89.250.195
150.216.144.82
241.25.212.52
187.150.175.127
~~~
***
### Exercise 36
36) Найти все активные хосты использую/не используя nMAP в: 
- заданной сети 
~~~
vagrant@ubuntu-xenial:~$ echo 10.23.106.{1..254} | xargs -n1 -P0 ping -c1|grep "bytes from" | grep -E -o "([0-9]{1,3}[\.]){3}[0-9]{1,3}"
10.23.106.15
10.23.106.3
10.23.106.5
10.23.106.4
10.23.106.6
10.23.106.10
10.23.106.14
10.23.106.7
10.23.106.9
10.23.106.13
10.23.106.8
10.23.106.11
10.23.106.12
10.23.106.16
10.23.106.17
10.23.106.18
10.23.106.19
10.23.106.22
10.23.106.24
10.23.106.46
~~~
- списке IP (hosts-server.txt) 
~~~
vagrant@ubuntu-xenial:~$ cat /etc/hosts | grep -E -o "([0-9]{1,3}[\.]){3}[0-9]{1,3}" | xargs -n1 -P0 ping -c1 | grep "bytes from" | grep -E -o "([0-9]{1,3}[\.]){3}[0-9]{1,3}"
127.0.0.1
127.0.1.1
~~~
- заданной сети
~~~
vagrant@ubuntu-xenial:~$ nmap -sn -oG - -v 192.168.0.0/24 | grep 'Status: Up'
Host: 10.23.106.8 ()  Status: Up
Host: 10.23.106.22 ()  Status: Up
~~~
- списке IP (hosts-server.txt)
~~~
vagrant@ubuntu-xenial:~$ nmap -sn -oG - -v $(cat /etc/hosts | grep -E -o "([0-9]{1,3}[\.]){3}[0-9]{1,3}") | grep 'Status: Up'
Host: 127.0.0.1 (localhost)     Status: Up
Host: 127.0.1.1 (task1) Status: Up
~~~
***
### Exercise 37
37) Получить все поддомены из SSL сертификата.
~~~
vagrant@ubuntu-xenial:~$ openssl x509 -text -noout -in /etc/ssl/certs/*.crt | grep -oP '[a-z0-9]+\.[a-z]+\.[a-z]+' | cut -d. -f1
www
ocsp
www
www
~~~