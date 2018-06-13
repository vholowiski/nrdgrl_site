---
layout: post
title: How to use chmod and chown
categories: Linux,RHEL/CentOS
---

How to use chmod and chown
## Note: This post is a work in progress. I'm posting what I have so far in case it helps you out.

UNIX permissions. Love them or hate them, if you're working on a Linux server, before long you're going to have to work with them. I can help.

Before we get started, open up a shell and you can follow along. Type `cd` and hit enter to make sure you're in your home directory, then type `touch permissions.txt` to create a blank file.

Before we start changing them, let's have a look at this file's existing permissions. To see file permissions, use the -l switch for ls.
`ls -l`
and you should get something like this:
`-rw-rw-r--. 1 username username 0 Aug 1 06:50 permissions.txt`
The first part `-rw-rw-r--.` are the file permissions. Yours might look slightly different - the permissions new files are created with depend on your UMASK (which is essentially your default permissions - I'll explain in another tutorial). This string can be divided into 5 parts- the first character specifies file type (normal or special). The next 3 characters `rw-`are the user permissions, the next 3 are the group permissions, the next 3 are the world permissions, and the last character has to do with ACL's.

**File Type:** **-**rw-rw-r--.

In this case the first character is a dash. That means that this is a regular file. If this were a directory, the permissions might look like this:`drwxr-xr-x.` - the first character is a d, for directory. This might also be an l (like Larry) if the file is a link. Note that you can't change this attribute, it's just an indicator.

**Owner Permissions:** -**rw-**rw-r--.

The next three characters are the user, or Owner permissions. These are the permissions for the current owner (in this case, also the creator) of the file. If you look at the full output of ls -l, the user is the name after the 1 (bolded below)
`-rw-rw-r--. 1 **username** username 0 Aug 1 06:50 permissions.txt`
There are three permissions that can be granted: **R**ead, **W**rite, and e**X**ecute. In this case, the owner has permission to Read the file, and Write to the file, but not to execute the file. Since this is a text file, we don't want to execute it (and it could be a security issue if it was executable), but if it was a shell script, we might want to change it to be executable.

**Group, and World:** -rw-**rw-r--**.

The second and third parts of the permissions are the group permissions and the world permissions. In this case, the group name is the same as the user name

-rw-rw-r--. 1 username **username** 0 Aug 1 06:50 permissions.txt