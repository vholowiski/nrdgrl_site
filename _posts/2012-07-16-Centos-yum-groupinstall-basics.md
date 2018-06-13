---
layout: post
title: CentOS yum groupinstall Basics
categories: RHEL/CentOS
---
If you've been using CentOS or Red Hat Enterprise Linux (RHEL) for long, you're no doubt familiar with the package manager - yum. Yum is a great package manager (random trivia, do you know what YUM stands for? - Yellow Dog Updater, Modified.) but it has some great features that you might not be using yet.

Today we're going to talk about yum groupinstall, a great way to install a large group of packages, to prepare your CentOS system for a specific task. So what can you install using the yum groupinstall command? That actually brings us to our first command:

```
yum grouplist
```

You could also type:

```
yum grouplist | less
```

so that you can scroll through the list page by page.

When you type this command, you will get a list of all of the package groups that are both installed, and installable. Have a look at the names. Remember when you installed CentOS, and you selected the "Desktop" or the "Web Server" check-box (or de-selected them)? What you were really doing was telling the installer to install a specific yum package group. Let me show you a few commands I use all the time (especially when setting up a new CentOS web server).

```
yum groupinstall "Development Tools"
```

Note that because there are spaces in many of the group names, they have to be enclosed in quotes, as above. This command will install all of the necessary linux development tools. This is great if you need to compile some software (like Ruby) and you're starting with a bare system. No need to install dozens of packages manually. When I ran this command, it offered to install 102 packages for me.

Another group of groups that I use often are when setting up a web server:

```
yum groupinstall "Web Server"
yum groupinstall "MySQL Database client"
yum groupinstall "MySQL Database server"
yum groupinstall "PHP Support"
```

You can also combine groups in one command. So you could type the following command, and then go for coffee:

```
yum groupinstall "Web Server" "MySQL Database client" "MySQL Database server" "PHP Support" -y
```

Also note the `-y` at the end of the command. This simply answers the <code>"Is this OK"</code> question, so you don't have to hit Y to install the packages.

This group of commands basically installs everything that you need to have a functioning web server (it doesn't configure it though, you'll still have to start the services, configure apache, secure mysql etc) and will save you a huge amount of time. There is another related command that's very useful. Try typing:

```
yum groupinfo "Web Server" | less
```

You'll get a nice list of "mandatory packages", "default packages", and "optional packages". Note that this is not everything that will be installed. When you run the groupinstall command, yum will also figure out all of the dependencies, and install all the packages that are required.

There are a few other Group commands that are worth knowing about:

* `yum groupremove "Group Name"` - will remove all of the packages in the specified group (but does not remove the dependencies, that would be bad).
* `yum groupupdate "Group Name"` - updates the packages in the specified group (yum groupinstall would do the same thing)

That's all for the yum groupinstall command, now go give it a try!