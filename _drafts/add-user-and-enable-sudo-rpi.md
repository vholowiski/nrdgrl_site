Adding a user and enabling sudo on raspberry pi raspbian

Open a terminal as pi (remember the default sudo password is raspberry - but hopefully you've changed that!)

sudo adduser username

Adding user `vholowiski' ...
Adding new group `vholowiski' (1001) ...
Adding new user `vholowiski' (1001) with group `vholowiski' ...
Creating home directory `/home/vholowiski' ...
Copying files from `/etc/skel' ...
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
Changing the user information for vholowiski
Enter the new value, or press ENTER for the default
        Full Name []: Victoria Holowiski
        Room Number []:
        Work Phone []:
        Home Phone []:
        Other []:
Is the information correct? [Y/n] Y

give the user sudo access
sudo usermod -aG sudo vholowiski

Test the new user- first log in as them:
su - username

vholowiski@vpi:~ $ sudo ls -al

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

[sudo] password for vholowiski:

total 24
drwxr-xr-x 2 vholowiski vholowiski 4096 Jun 13 17:26 .
drwxr-xr-x 4 root       root       4096 Jun 13 17:24 ..
-rw------- 1 vholowiski vholowiski    5 Jun 13 17:26 .bash_history
-rw-r--r-- 1 vholowiski vholowiski  220 Jun 13 17:24 .bash_logout
-rw-r--r-- 1 vholowiski vholowiski 3523 Jun 13 17:24 .bashrc
-rw-r--r-- 1 vholowiski vholowiski  675 Jun 13 17:24 .profile

Optional but highly recommended - delete the original pi user
	* note that this will delete the pi home directory too, and anything you've put there (in /home/pi)
sudo deluser -remove-home pi

vholowiski@vpi:~ $ sudo deluser -remove-home pi
Looking for files to backup/remove ...
Removing files ...
Removing user `pi' ...
Warning: group `pi' has no more members.
userdel: user pi is currently used by process 22993
/usr/sbin/deluser: `/usr/sbin/userdel pi' returned error code 8. Exiting.
- if so:
vholowiski@vpi:~ $ sudo who -u
pi       pts/0        2018-06-13 17:23   .         22987 (184.69.202.238)
vholowiski@vpi:~ $ kill 22987
-su: kill: (22987) - Operation not permitted
vholowiski@vpi:~ $ sudo kill 22987
Connection to 172.103.179.69 closed by remote host.
Connection to 172.103.179.69 closed.


