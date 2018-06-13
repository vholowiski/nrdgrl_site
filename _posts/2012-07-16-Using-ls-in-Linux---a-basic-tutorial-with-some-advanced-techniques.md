---
layout: post
title: Using ls in Linux, a basic tutorial with some Advanced techniques
categories: RHEL/CentOS
---

Of any Linux command, ls is probably the most used (note that's l as in Lima, s as in Sierra, both lower case). The man page (type `man ls`) says that the command "lists directory contents". This is true, but greatly understates the usefulness of this command. Most likely when you type the ls command, you'll get something like this:

```
[root@beast ~]# ls
anaconda-ks.cfg                 Desktop    Downloads    install.log.syslog  Pictures  Templates
CentOS-6.2-x86_64-bin-DVD1.iso  Documents  install.log  Music               Public    Videos
```

A listing of the files in that directory, nothing more. If you got something different, don't worry- probably an alias has been set to make the ls command do something different. I'll show you how to do that later.

But ls isn't showing you everything. In Linux (and Unix in general) a file is considered a 'hidden' file if it starts with a period `.` and ls doesn't show you hidden files by default. However, typing `ls -a` will show you **a**ll the files in that directory, including ones that start with a `.` There are two special entries in every directory: `.` and `..`. One period is a reference to the current directory, and two periods is a reference to one directory up in the file hierarchy. If you type `ls -A` - the capital A means "almost all", the `.` and `..` will be omitted from the listing.

Another simple option is to show color. This is usually 'turned on' by default, and it shows directories and files in different colors (directories are usually blue). The command is `ls --color`. Typing this probably won't change anything for you, because it's probably already being shown that way. However, let's say that you like a neat and tidy listing and prefer to have all the directories listed first, not mixed in with the files all willy nilly. Type: `ls --group-directories-first` and you'll have your wish.

You've also got some really good sorting options. `ls -S` will sort the files by their size, `ls -t` will sort them by their modification time, and `ls -X` will sort them by their extension (alphabetically). Adding `-r` to any of these commands will reverse the order.

Which brings up an important point- you can use more than one switch at a time, just blob them all together. So to show all files by size reverse order, type `ls -aSr --group-directories-first --color` - note that single letters can be combined, but commands that start with a double dash `--` must be separate.

So far all of the listings have been in column view (probably - unless your system has already been customized). But I find list view much more useful, as it presents more useful information. To get a list view type `ls -l` (that's a lower case l as in Lima). This gives you a vertical listing of files. The first 4 colums are UNIX Permissions - something I don't have time to go into here - and then the file size, date/time of the last modification, and the file name. See the example below.
```
[root@beast ~]# ls -l
total 4319572
-rw-------. 1 root root       1768 Jun 24 15:05 anaconda-ks.cfg
-rw-r--r--. 1 qemu qemu 4423129088 Dec 15  2011 CentOS-6.2-x86_64-bin-DVD1.iso
drwxr-xr-x. 2 root root       4096 Jun 24 15:11 Desktop
drwxr-xr-x. 2 root root       4096 Jun 24 15:11 Documents
drwxr-xr-x. 2 root root       4096 Jun 24 17:14 Downloads
-rw-r--r--. 1 root root      51685 Jun 24 15:05 install.log
-rw-r--r--. 1 root root      11621 Jun 24 15:02 install.log.syslog
drwxr-xr-x. 2 root root       4096 Jun 24 15:11 Music
drwxr-xr-x. 2 root root       4096 Jun 24 15:11 Pictures
drwxr-xr-x. 2 root root       4096 Jun 24 15:11 Public
drwxr-xr-x. 2 root root       4096 Jun 24 15:11 Templates
drwxr-xr-x. 2 root root       4096 Jun 24 15:11 Videos
```
But I have one problem with this view - file sizes are shown in bytes. That's fine for computers, but I am a human, so I use the -h switch `ls -lh`, which gives me file sizes in K, M, and G (Kilobytes, Megabyes and Gigabytes)
```
[root@beast ~]# ls -lh
total 4.2G
-rw-------. 1 root root 1.8K Jun 24 15:05 anaconda-ks.cfg
-rw-r--r--. 1 qemu qemu 4.2G Dec 15  2011 CentOS-6.2-x86_64-bin-DVD1.iso
drwxr-xr-x. 2 root root 4.0K Jun 24 15:11 Desktop
drwxr-xr-x. 2 root root 4.0K Jun 24 15:11 Documents
drwxr-xr-x. 2 root root 4.0K Jun 24 17:14 Downloads
-rw-r--r--. 1 root root  51K Jun 24 15:05 install.log
-rw-r--r--. 1 root root  12K Jun 24 15:02 install.log.syslog
drwxr-xr-x. 2 root root 4.0K Jun 24 15:11 Music
drwxr-xr-x. 2 root root 4.0K Jun 24 15:11 Pictures
drwxr-xr-x. 2 root root 4.0K Jun 24 15:11 Public
drwxr-xr-x. 2 root root 4.0K Jun 24 15:11 Templates
drwxr-xr-x. 2 root root 4.0K Jun 24 15:11 Videos
```
Now that we've gotten this far, I'll tell you my preference for the ls command - it's `ls -alht --color --group-directories-first` - that's a mouthfull! Don't worry we'll fix that later, first there is one last switch I want to mention: -Z `ls -Z`. That will give you something crazy like this:
```
[root@beast ~]# ls -Z
-rw-------. root root system_u:object_r:admin_home_t:s0 anaconda-ks.cfg
-rw-r--r--. qemu qemu system_u:object_r:virt_content_t:s0 CentOS-6.2-x86_64-bin-DVD1.iso
drwxr-xr-x. root root system_u:object_r:admin_home_t:s0 Desktop
drwxr-xr-x. root root system_u:object_r:admin_home_t:s0 Documents
drwxr-xr-x. root root system_u:object_r:admin_home_t:s0 Downloads
-rw-r--r--. root root system_u:object_r:admin_home_t:s0 install.log
-rw-r--r--. root root system_u:object_r:admin_home_t:s0 install.log.syslog
drwxr-xr-x. root root system_u:object_r:admin_home_t:s0 Music
drwxr-xr-x. root root system_u:object_r:admin_home_t:s0 Pictures
drwxr-xr-x. root root system_u:object_r:admin_home_t:s0 Public
drwxr-xr-x. root root system_u:object_r:admin_home_t:s0 Templates
drwxr-xr-x. root root system_u:object_r:admin_home_t:s0 Videos
```
The extra columns that it is showing are security contexts for SELinux. You do use SELinux don't you? What you disabled it? Keep your eyes open for a SELinux tutorial - anybody who's running a web server should be using SELinux! Once you start using it, you'll no doubt find the -Z command very helpful.

By now, you probably see some options (they're actually called switches) that you want to use all the time. Maybe like me you want to use `ls -alht --color --group-directories-first` or some variation of that. If you typed that every time instead of `ls` you're going to wear your keyboard, and your fingers, out. Fortunately, Linux was built by and for lazy people. There are a few things you can do. The first is to create a temporary alias. This will exist until you log out of your account. To create an alias for my favorite command, type
```
alias ls="ls -alht --color --group-directories-first"
```
and hit enter. Now, instead of executing ls when you type ls, your computer will execute `ls -alht --color --group-directories-first` - until you log out and back in, that is.

If you want that alias to endure - so it's always there, you have to edit your .bashrc file. This file is located in your home directory. If you're signed in as root, that's under /root/.bashrc - if you're signed in as a user it's under ~/.bashrc (note that the ~/ is special and always points to your home directory). So if you edit the `~/.bashrc` file, you'll probably see 3 alias commands there already - mine are:
```
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
```
Just add your new alias command to the bottom of the list. You'll need to log out and back in for this new alias to take effect. _Note, I'm not telling you how to edit the file. If you don't know how to do that, you shouldn't be doing it. I'll post a tutorial on how to edit files sometime_.

There you go, ls in a nutshell. I hope that helped. Please post feedback below, including your favorite ls tricks, or any questions or comments you have!