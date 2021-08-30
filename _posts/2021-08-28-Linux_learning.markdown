---
layout: default
title:  "Linux green hand"
date:   2021-08-28 19:44:39 +0800
categories: Linux
---

# Background

Recently I found my Linux foundation rather weak, and felt it cool to have a good command of Linux, so I begin to learn Linux by reading *The Linux Command Line: A Complete Introduction* by William Shotts.



# Linux Commands

1. check the current amount of free space of disk drives: `df -h`

2. `ls` : `-t -S`: sort by time or size `-r`: reverse order `-h`: human readable, `-d` only directory

3. ==Attention:== options in Linux are case sensitive

4. use `file` to check the type of the file, use `less` to check the content of the text file, `stat` can give more information on the file

5. symbolic links: for a typical symlink: `lrwxrwxrwx 1 root root 11 2018-08-11 07:34 libc.so.6 -> libc-2.6.so` ,  `libc-2.6.so` is the original file, while the symlink `libc.so.6` pointing to it can be changed

   ```shell
   ln -s item link # Create a symlink
   # when we create a symbolic link, we are creating a text Chapter 4description of where the target file is relative to the symbolic link.
   ln -s ../fun dir1/fun-sym 
   ln -s absolute_path sym
   # symlink can be used on the dir
   
   ```

6. hardlink:

   ```shell
   ls -li
   12353538 -rw-r--r-- 4 me me ... fun
   12353538 -rw-r--r-- 4 me me ... funhard
   # inode number suggests fun and funhard share the same content 
   # 4 means fun has 4 hardlinks
   ```

7. wildcard: 

   ```shell
   *
   ? 
   [characters] 
   [!characters] 
   [[:class:]]
   # Wild card always expand in sorted order
   ```

8. ```shell
   cp item... directory
   # -a(copy with attributes) -i(interactive) -r -u update 
   #mv rm has nearly the same usage of cp
   #but mv has no option -r
   mv dir1 dir2
   ```

9. The essence of the commands:

   * An executable program

   * A command built into the shell itself

   * A shell function

   * An alias

     `type` is used to identify four commands  `which` is used to find out the executable program

10. `alias`

    ```shell
    alias name="string" #no white-space allowed
    unalias name
    # Attention: alias defined in the shell will end after the sessio
    ```

11. redirection and pipe

    ```shell
    # redirect output to a txt file using > will always overwrite origin file, so we have the trick
    $ > output.txt # to clear the content of the txt file
    # >> will append rather than overwrite
    # redirect error error
    ls -l /bin/usr 2> ls-error.txt # 2 is called file descriptor, 
    ls -l /bin/usr &> ls-output.txt # both stderr and stdout
    # can also use 2>> nad &>>
    ls -l /bin/usr &> /dev/null 
    cat file1 file2 > file#if there are no file1,file2, then cat get input from stdin, if there is no >, cat output to the stdout
    cat < file1 #equal to `cat file1`
    ls -l /usr/bin | less
    ```

12. Filters

    ```shell
    # commands used in pipe to process is called filters
    ls /usr/bin | sort | less
    ls /usr/bin /bin | sort | uniq | less
    ls /usr/bin /bin | sort | uniq | less | wc -l
    grep pattern filename
    ls /usr/bin /bin | sort | uniq | grep zip
    # grep -i: ignore case grep -v:print lines without pattern
    ls /usr/bin | tail -n 5
    # Attention, many commands don't accept the stdin, for example
    which cp | ls #don't work, use
    which cp | xargs ls -l #instead, however, use command substituion is more common
    ```

    It seems that commands with the pattern  `command file` can always be transformed into the form `command someinput > someoutput`

13. tee

    ```shell
    # tee can be seen as a "tee" for the pipe
    ls /usr/bin | tee ls.txt | grep zip
    ```


14. Shell expansion: Most important features of shell command

    ```shell
    # pathname expansion for wildcard and tilde
    echo .[!.]*
    # arithmetic expansion
    echo $(((3**2)+2)) #Attention to the first parenthesis
    # Barce expansion -- important preamble{expansion contents}postscript
    echo Front-{A,B,C}-Back
    echo Number_{1..5} # Attention TWO dots here!!!
    echo a{A{1,2},B{3,4}}b #nested
    echo a{1..10}-{1..12}
    # parameter expansion
    echo $USER
    # command substitution
    ls -l $(which cp)
    file $(ls -d /usr/bin/* | grep zip)
    ```

15. quotes

    ```shell
    # Double quotes suppress word splitting, wildcard, tilde, barce expansion but do nothing to $ / `
    # Single quotes suppress all the expansion
    # Escaping characters are used to quote one characters using \
    # \ can be used as control code
    \a \t
    ```



# Keyboard tricks

bash uses a library (a shared collection of routines that different programs can use) called Readline to implement command line editing. Here are useful tricks to ease the pain of stroke

## Cursor Movement

`ctrl A/E`: move to the front/back of a line

`ctrl/alt F/B `: move cursor forward/backward a character/word

`ctrl L`: clear

## Modify the text

`ctrl D`: delete the character

`ctrl K/U`: kill the text from cursor to end/beginning of line

`ctrl Y`: yank 

## Use history

```shell
history | grep pattern
!88 #history expansion
```



# Permissions

## wrx

For files, wrx decides whether a file can be opened, written, or executed.  The difficult part is to understand the effect on the directory.

For directory, r allows a directory's contents to be listed if x is also set. w allows files within a directory to be created, deleted, and renamed if x is set. x allows a directory to be entered.

## chmod chown

```shell
#chmod can be used in two ways : octal and symbolic
#for octal, each wrx is mapped to three binary and then transformed to an octal
000 -> ---  001 -> --x 
chmod 600 test.txt
# symbolic format is sym1+sym2 or sym1=sym2, no white space permitted
#sym1 can be u,g,o,a,sym2 is wrx
chmod u+x test.txt
chown [owner][:[group]] file...
# typical usage
chown wbc file1
chown wbc:thu fil1 
chown :thu file1 # owenr remains the same
chown wbc: file1 # chage group to the login group of wbc
```

## umask

```shell
# umask is set to change the default permissions, by default, the permission is rw-rw-rw-
umask 0000
# the last three octal number is used to reverse the default set, the first octal number has special effect
```

## Identity

```shell
# command su allows you to asuume the identity of another user and launch a new shell
su [-[l]] [user]
# -l or - will make this shell session a login session, all environment will be reloaded and directory will be changed to user's home
# if user is omitted, it menas super
```

#### More on sudo: 

sudo command is actually configured to allow an ordinary user to execute commands as a different user(always superuser). Namely, only commands are executed as another user, all environment remains the same, and authenticating uses the users' password rather than super user's

#### Learn some history

To understand the history of `su` and `sudo` is of great help to understand the identity. 

To give the users the rights to install or do something, most Linux distributions relied on `su`, `su` didn’t require the configuration that `sudo` required, and having a root account is traditional in Unix. This tempted the user to always operate as root user, which is no secure.

When Ubuntu was introduced, its creators took a different tack. By default, Ubuntu disables logins to the root account (by failing to set a pass-
word for the account) and instead uses sudo to grant superuser privileges. The initial user account is granted full access to superuser privileges via sudo and may grant similar powers to subsequent user accounts.







# Processes

## View processes

```shell
#ps is used to view the processes, without option, it will give processes in this session
PID  TTY  TIME CMD
#TTY is "teletype", refers to the controlling terminal for the processes.
ps -x # give all the processes 
ps aux # give more information
top # give a dynamic monitor of the process rather than a snapshot
```

## Control processes

```shell
# if we execute a program in the terminal with &, it will background the process
typora test.md &
jobs # list the job launched from terminal
fg %1 # return a process to the foreground, 1 is the jobspec
bg %1 # make it run at the background 
# ctrl c terminate the process while the ctrl z only suspend the process
# launch a program from the command line will print some error messages rather helpful
```

## Signals

```shell
# kill send signals to programs
kill -signal PID...
# typical signal 
INT # interrupt ctrl-C
TERM # terminate
STOP #
TSTP # ctrl - Z
CONT # continue
kill -INT 13601
# kill with no signals send TERM
# killall is used tosend signals to multiple processes matching a specified program or username
# poweroff halt reboot can be used without options
# shutdown can be used as the above three commands
sudo shutdown -h now
sudo shutdown -r now
```



# Environment

```shell
printenv | less # only display environment variables
set | less # display both shell and environment variables
```

Every time we login a shell it will read the config files. For ubuntu, it will read `/etc/profile`, `/etc/bash.bashrc`,  `~/.profile`, `~/.bashrc`

`PATH` variable is often set by the */ect/profile*  

`export $var` tellls the shell to make the contents of var available to child processes of this shell

Add `PATH` of define additional environment variables change *.profile*, for else change *.bashrc*

 `source` force the shell to read the new config file  



# Package Management

Linux software workflow: 

*upstream provider*(program's author) -> *package maintainer*(compile source code and improve it to better fit the other part of the system)-> distribution vendor -> Central Repositories 

A distribution will not only have many central repositories, but also have some third-party repositories of legal or other reasons.

*Dependency resolution* is to find the dependency of a software and install them together

High-level tools handle tasks such as installing and removing, while low-level tools perform metadata searching and dependency resolution

Linux distribution is divided into two parts concerning about the package management: Debian-style(Ubuntu), Red-Hat style(CentOS, Redora), the former uses `dpkg` as low level and `apt-get apt apttude` as high level

```shell
# to search a package. serach the package metadata and download from the apt repository
apt-get update
apt-cache search package-name
# use low-level tool
dpkg -i package-file # Attention, this is installed without dependency resolution
# list packages installed
dpkg -l
# display the information of an installed package
apt-cache show package_name
# find which package isntalled a file
dpkg -S file_name 
```



# Network

```shell
ping google.com
traceroute google.com
```





# Basic skills

## Searching for files

`locate` performs a database search of pathnames(so it is based solely on the name), it can be combined with `grep`.

`find` search a directory and its subdirectories based on the attributes `tests`, `options`, `actions`

```shell
# Tests
find ~ -type d | wc -l # d for dir, f for regular file, l for symbolic link
find ~ -type f -name "*.JPG" -size +1M | wc -l
# -type -empty -name -size are called tests, there are many different tests can be used
# logic operator can be used to make tests more powerful
find ~ \( -type f -not -perm 0600\) -or \( -type d -not -perm 0700 \) # Attention the \ here
# Logical operator has short-circuit property
```

```shell
# Actions
find -type f -name '*.bak' -delete # -print -delete -ls are pre-defined actions
# every test and action are actually connected by -and
# user-defined actions
-exec command {} ; # -exec can be changed with -ok to make a confirm
find ~ -type f -name 'foo*' -ok ls -l '{}' ';' # Attention the single quote here
```

```shell
# Options
# it seems that options are not that frequently used, so I don't take themdown
```

## Archiving and Backup



 

