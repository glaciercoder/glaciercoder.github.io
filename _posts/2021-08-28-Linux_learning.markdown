---
layout: default
title:  "Linux green hand"
date:   2021-08-28 19:44:39 +0800
categories: Linux
---

# Background

Recently I found my Linux foundation rather weak, and feel it cool to have a good command of Linux, so I begin to learn Linux by reading *The Linux Command Line: A Complete Introduction* by William Shotts.



## Linux Shell

1. check the current amount of free space of disk drives: `df -h`

2. `ls` : `-t -S: sort by time or size `-r`: reverse order `-h`: human readable

3. ==Attention:== options in Linux are case sensitive

4. use `file` to check the type of the file, use `less` to check the content of the text file

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

11. redirection

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
    ```

    It seems that commands with the pattern  `command file` can always be transformed into the form `command someinput > someoutput`

13. tee

    ```shell
    # tee can be seen as a "tee" for the pipe
    ls /usr/bin | tee ls.txt | grep zip
    ```

    
