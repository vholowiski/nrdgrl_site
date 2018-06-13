---
layout: post
title: Adding a User and enabling Sudo on a Raspberry Pi (raspbian)
---
If you've just installed Raspbian on your shiny new Raspberry Pi and enabled SSH, it's open to the world. You really, *really* want to set up a new user and delete the pi user.

To do this: 
* Open a terminal as pi (remember the default sudo password is raspberry - but hopefully you've changed that!) and type

```
sudo adduser username
```
Result:

```
Adding user `username' ...
Adding new group `username' (1001) ...
Adding new user `username' (1001) with group `username' ...
Creating home directory `/home/username' ...
Copying files from `/etc/skel' ...
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
Changing the user information for username
Enter the new value, or press ENTER for the default
        Full Name []: My Name
        Room Number []:
        Work Phone []:
        Home Phone []:
        Other []:
Is the information correct? [Y/n] Y
```

Now give the user sudo access so you can do things as root:s

```
sudo usermod -aG sudo username
```

Test the new user- first log in as them:

```
su - username
sudo ls -al

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

[sudo] password for username:

total 24
drwxr-xr-x 2 username username 4096 Jun 13 17:26 .
drwxr-xr-x 4 root       root       4096 Jun 13 17:24 ..
-rw------- 1 username username    5 Jun 13 17:26 .bash_history
-rw-r--r-- 1 username username  220 Jun 13 17:24 .bash_logout
-rw-r--r-- 1 username username 3523 Jun 13 17:24 .bashrc
-rw-r--r-- 1 username username  675 Jun 13 17:24 .profile
```

Optional but highly recommended - delete the original pi user
  * note that this will delete the pi home directory too, and anything you've put there (in /home/pi)

```
sudo deluser -remove-home pi

Looking for files to backup/remove ...
Removing files ...
Removing user `pi' ...
Warning: group `pi' has no more members.
```

You're done. Enjoy your slightly more secure Raspberry Pi

