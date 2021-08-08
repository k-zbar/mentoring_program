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
- Echo a different full sentence, but redirect it to /dev/null__
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
- Evaluate another arithmetic expression
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
Найти дубликаты файлов в заданных каталогах. Вначале сравнивать по размеру, затем по варианту (выбрать хешь функцию: CRC32, MD5, SHA-1, sha224sum). Результат должен быть отсортирован по имени файла. 
~~~
vagrant@ubuntu-xenial:~/task_5$ cat file1.txt file2.txt file3.txt file4.txt
Hello world
Here is string
Hello world
Pretty good
~~~
~~~
vagrant@ubuntu-xenial:~/task_5$ find . -type f -exec du -h {} \; | sort
4.0K    ./file1.txt
4.0K    ./file2.txt
4.0K    ./file3.txt
4.0K    ./file4.txt
~~~
***
### Exercise 7
Найти по имени файла и его пути все символьные ссылки на него. 
~~~
vagrant@ubuntu-xenial:~$ touch file7.txt
vagrant@ubuntu-xenial:~$ ln -s file7.txt f_link
vagrant@ubuntu-xenial:~$ ls -li
total 12
  2303 -rw-rw-r-- 1 vagrant vagrant    0 Feb 14 12:27 demo-dev
256069 drwxrwxr-x 3 vagrant vagrant 4096 Jun 12 22:26 demo-devops
   126 -rw-rw-r-- 1 vagrant vagrant    0 Jun 12 22:47 file7.txt
   129 lrwxrwxrwx 1 vagrant vagrant    9 Jun 12 22:47 f_link -> file7.txt
   122 -rw-rw-r-- 1 vagrant vagrant  536 Jun 12 21:00 out.txt
256035 drwxrwxr-x 2 vagrant vagrant 4096 Jun 12 22:42 task_5
~~~
~~~
vagrant@ubuntu-xenial:~$ find -lname file7.txt
./f_link
~~~
***
### Exercise 8
Найти по имени файла и его пути все жесткие ссылки на него. 
~~~
vagrant@ubuntu-xenial:~$ touch file8.txt
vagrant@ubuntu-xenial:~$ ln file8.txt f_h_link
vagrant@ubuntu-xenial:~$ ls -li
total 12
  2303 -rw-rw-r-- 1 vagrant vagrant    0 Feb 14 12:27 demo-dev
256069 drwxrwxr-x 3 vagrant vagrant 4096 Jun 12 22:26 demo-devops
  1387 -rw-rw-r-- 2 vagrant vagrant    0 Jun 12 23:35 f_h_link
   126 -rw-rw-r-- 1 vagrant vagrant    0 Jun 12 22:47 file7.txt
  1387 -rw-rw-r-- 2 vagrant vagrant    0 Jun 12 23:35 file8.txt
   129 lrwxrwxrwx 1 vagrant vagrant    9 Jun 12 22:47 f_link -> file7.txt
   122 -rw-rw-r-- 1 vagrant vagrant  536 Jun 12 21:00 out.txt
256035 drwxrwxr-x 2 vagrant vagrant 4096 Jun 12 22:42 task_5
~~~
~~~
vagrant@ubuntu-xenial:~$ find -samefile file8.txt
./f_h_link
./file8.txt
~~~
***
### Exercise 9
Имеется только inode файла найти все его имена. 
~~~
vagrant@ubuntu-xenial:~/task9$ touch file9.txt
vagrant@ubuntu-xenial:~/task9$ ln file9.txt h_file9.txt
vagrant@ubuntu-xenial:~/task9$ ls -li
total 0
277177 -rw-rw-r-- 2 vagrant vagrant 0 Jun 12 23:51 file9.txt
277177 -rw-rw-r-- 2 vagrant vagrant 0 Jun 12 23:51 h_file9.txt
~~~
~~~
vagrant@ubuntu-xenial:~$ find -inum 277177
./task9/file9.txt
./task9/h_file9.txt
~~~
***
### Exercise 10
Имеется только inode файла найти все его имена. Учтите, что может быть примонтированно несколько разделов.
~~~
vagrant@ubuntu-xenial:~$ find -mount -inum 277177
./task9/file9.txt
./task9/h_file9.txt
~~~
***
### Exercise 11
Корректно удалить файл с учетом возможности существования символьных или жестких ссылок.
~~~
vagrant@ubuntu-xenial:~$ ls -li
total 16
  2303 -rw-rw-r-- 1 vagrant vagrant    0 Feb 14 12:27 demo-dev
256069 drwxrwxr-x 3 vagrant vagrant 4096 Jun 12 22:26 demo-devops
  1387 -rw-rw-r-- 2 vagrant vagrant    0 Jun 12 23:35 f_h_link
   126 -rw-rw-r-- 1 vagrant vagrant    0 Jun 12 22:47 file7.txt
  1387 -rw-rw-r-- 2 vagrant vagrant    0 Jun 12 23:35 file8.txt
   129 lrwxrwxrwx 1 vagrant vagrant    9 Jun 12 22:47 f_link -> file7.txt
   122 -rw-rw-r-- 1 vagrant vagrant  536 Jun 12 21:00 out.txt
256035 drwxrwxr-x 2 vagrant vagrant 4096 Jun 12 22:42 task_5
277176 drwxrwxr-x 2 vagrant vagrant 4096 Jun 12 23:51 task9
~~~
~~~
vagrant@ubuntu-xenial:~/task9$ ls
file9.txt  h_file9.txt
vagrant@ubuntu-xenial:~/task9$ rm $(find -samefile file9.txt && find -lname h_file9.txt)
vagrant@ubuntu-xenial:~/task9$ ls -li
total 0
~~~
***
### Exercise 12
Рекурсивно изменить права доступа к файлам (задана маска файла) в заданной директории.
~~~
vagrant@ubuntu-xenial:~$ ll -Rl task12/
task12/:
total 16
drwxrwxr-x  4 vagrant vagrant 4096 Jun 13 00:08 ./
drwxr-xr-x 10 vagrant vagrant 4096 Jun 13 00:08 ../
drwxrwxr-x  2 vagrant vagrant 4096 Jun 13 00:08 1/
drwxrwxr-x  2 vagrant vagrant 4096 Jun 13 00:09 2/

task12/1:
total 8
drwxrwxr-x 2 vagrant vagrant 4096 Jun 13 00:08 ./
drwxrwxr-x 4 vagrant vagrant 4096 Jun 13 00:08 ../
-rw-rw-r-- 1 vagrant vagrant    0 Jun 13 00:08 123

task12/2:
total 8
drwxrwxr-x 2 vagrant vagrant 4096 Jun 13 00:09 ./
drwxrwxr-x 4 vagrant vagrant 4096 Jun 13 00:08 ../
-rw-rw-r-- 1 vagrant vagrant    0 Jun 13 00:09 321
~~~
~~~
vagrant@ubuntu-xenial:~$ find . -type f -name '*' -exec chmod +x {} \;
vagrant@ubuntu-xenial:~$ ll -Rl task12/
task12/:
total 16
drwxrwxr-x  4 vagrant vagrant 4096 Jun 13 00:08 ./
drwxr-xr-x 10 vagrant vagrant 4096 Jun 13 00:08 ../
drwxrwxr-x  2 vagrant vagrant 4096 Jun 13 00:08 1/
drwxrwxr-x  2 vagrant vagrant 4096 Jun 13 00:09 2/

task12/1:
total 8
drwxrwxr-x 2 vagrant vagrant 4096 Jun 13 00:08 ./
drwxrwxr-x 4 vagrant vagrant 4096 Jun 13 00:08 ../
-rwxrwxr-x 1 vagrant vagrant    0 Jun 13 00:08 123*

task12/2:
total 8
drwxrwxr-x 2 vagrant vagrant 4096 Jun 13 00:09 ./
drwxrwxr-x 4 vagrant vagrant 4096 Jun 13 00:08 ../
-rwxrwxr-x 1 vagrant vagrant    0 Jun 13 00:09 321*
~~~
***
### Exercise 13
13) Сравнить рекурсивно две директории и отобразить только отличающиеся файлы. * (вывести до 2 строки и после 3 строки относительно строки в которой найдено отличие). 
~~~
vagrant@ubuntu-xenial:~$ tree task13/
task13/
├── folder1
│   ├── file1
│   ├── file2
│   ├── file3
│   └── sub_dir
│       └── file4
└── folder2
    ├── file1
    └── file2
~~~
~~~
vagrant@ubuntu-xenial:~/task13$ find . -type f -exec basename {} \; | sort | uniq -u
file3
file4
~~~
***
### Exercise 14
14) Получить MAC-адреса сетевых интерфейсов.
~~~
vagrant@ubuntu-xenial:~$ ifconfig | egrep "HWaddr " | cut -b 39-55
02:bb:f4:57:e9:87
08:00:27:c2:97:d0
~~~
***
### Exercise 15
15) Вывести список пользователей, авторизованных в системе на текущий момент. 
~~~
vagrant@ubuntu-xenial:~$ who
vagrant  pts/0        2020-06-12 20:43 (10.0.2.2)
~~~
***
### Exercise 16
16) Вывести список активных сетевых соединений в виде таблицы: тип состояния соединения и их количество. 
~~~
vagrant@ubuntu-xenial:~$ ss -t | tail -n +2 | tr -s " " | cut -d' ' -f1 | sort | uniq -c
      1 ESTAB
~~~
***
### Exercise 17
17) Переназначить существующую символьную ссылку.
~~~
vagrant@ubuntu-xenial:~/task17$ ln -s test1 file_link
vagrant@ubuntu-xenial:~/task17$ ll
total 8
drwxrwxr-x  2 vagrant vagrant 4096 Jun 13 00:24 ./
drwxr-xr-x 11 vagrant vagrant 4096 Jun 13 00:21 ../
lrwxrwxrwx  1 vagrant vagrant    5 Jun 13 00:24 file_link -> test1
-rw-rw-r--  1 vagrant vagrant    0 Jun 13 00:21 test1
-rw-rw-r--  1 vagrant vagrant    0 Jun 13 00:21 test2
~~~
~~~
vagrant@ubuntu-xenial:~/task17$ ln -sf test2 file_link
vagrant@ubuntu-xenial:~/task17$ ll
total 8
drwxrwxr-x  2 vagrant vagrant 4096 Jun 13 00:25 ./
drwxr-xr-x 11 vagrant vagrant 4096 Jun 13 00:21 ../
lrwxrwxrwx  1 vagrant vagrant    5 Jun 13 00:25 file_link -> test2
-rw-rw-r--  1 vagrant vagrant    0 Jun 13 00:21 test1
-rw-rw-r--  1 vagrant vagrant    0 Jun 13 00:21 test2
~~~
***
### Exercise 18
18) Имется список фалов с относительным путем и путем к каталогу в котором должна храниться символьная ссылка на файл. Создать символьные ссылки на эти файлы. 
~~~
vagrant@ubuntu-xenial:~$ tree dir1 dir2
dir1
├── file1
├── file2
└── file3
dir2
~~~
~~~
vagrant@ubuntu-xenial:~/dir2$ ln -s ../dir1/* /home/vagrant/dir2
vagrant@ubuntu-xenial:~$ tree dir1 dir2
dir1
├── file1
├── file2
└── file3
dir2
├── file1 -> ../dir1/file1
├── file2 -> ../dir1/file2
└── file3 -> ../dir1/file3
~~~
***
### Exercise 19
19) Скопировать директорию с учетом, что в ней существуют как прямые так относительные символьные ссылки на файлы и директории. Предполагается, что копирование выполняется for backup on a removable storage. (сделать в двух вариантах, без rsync и с rsync). 
~~~
vagrant@ubuntu-xenial:~$ tree links2 destination
links2
├── file
└── links
    ├── link -> ../file
    └── link2 -> ../file
destination
~~~
Без rsync
~~~
vagrant@ubuntu-xenial:~$ cp -r links2/* destination
vagrant@ubuntu-xenial:~$ tree links2 destination
links2
├── file
└── links
    ├── link -> ../file
    └── link2 -> ../file
destination
├── file
└── links
    ├── link -> ../file
    └── link2 -> ../file
~~~
C rsync
~~~
vagrant@ubuntu-xenial:~$ rsync -r -l links2/* destination
vagrant@ubuntu-xenial:~$ tree links2 destination
links2
├── file
└── links
    ├── link -> ../file
    └── link2 -> ../file
destination
├── file
└── links
    ├── link -> ../file
    └── link2 -> ../file
~~~
***
### Exercise 21
21) В директории проекта преобразовать все относительные ссылки в прямые.
~~~
vagrant@ubuntu-xenial:~/task21$ tree
.
├── file
└── sub1
    └── sub2
        └── s_link -> ../../file

2 directories, 2 files
~~~
~~~
vagrant@ubuntu-xenial:~/task21$ find ./ -type l -execdir bash -c 'ln -sfn "$(readlink -f "$0")" "$0"' {} \;
vagrant@ubuntu-xenial:~/task21$ tree
.
├── file
└── sub1
    └── sub2
        └── s_link -> /home/vagrant/task21/file

2 directories, 2 files
~~~
***
### Exercise 22
22) В директории проекта преобразовать все прямые ссылки в относительные для директории проекта.
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