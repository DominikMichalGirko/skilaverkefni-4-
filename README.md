# skilaverkefni-4-
Practice: Users and Groups 

 

1. Create the users Serena Williams, Venus Williams and Justine Henin, all of them 

with password set to stargate, with username (lower case!) as their first name, and 

their full name in the comment. Verify that the users and their home directory are 

properly created. 

 

useradd -m -c 'Serena Williams' serena 

 

useradd -m -c 'Venus Williams' venus 

 

useradd -m -c ' Justine Henin' justine 

 

tail -2 /etc/passwdserena:x:1008:1010:Serena Williams:/home/serena:/bin/shvenus:x:1009:1011:Venus Williams:/home/venus:/bin/bash 

 

2. Create a user called kornuser, give him the Korn shell (/bin/ksh) as his default 

shell. Log on with this user (on a command line or in a tty). 

 

useradd -s /bin/ksh kornuser ; passwd kornuser 
 

 

 

 

3. Create a user named einstime without home directory, give him /bin/date as his 

default logon shell. What happens when you log on with this user ? Can you think of 

a useful real world example for changing a user's login shell to an application? 

 

useradd -s /bin/date einstime 

su - einstime 

It can be useful when users needs to access only one application on the server. 

 

 

4. Try the commands who, whoami, who am i, w, id, echo $USER $UID . 

 

 

Whoami – dominik 

Id - uid=1000(dominik) gid=1000(dominik) groups=1000(dominik),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),120(lpadmin),132(lxd),133(sambashare) 

 

W - SER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT and more … 

 

 

echo $USER $UID – dominik 1000 

 

 

 

 

 

5a. Lock the venus user account with usermod. 

 

usermod -L venus 

 

5b. Use passwd -d to disable the serena password. Verify the serena line in /etc/ 

shadow before and after disabling. 

 

grep serena /etc/shadow | cut -c1-70 passwd -d serenapasswd: password expiry information changed.r grep serena /etc/shadow 

 

5c. What is the difference between locking a user account and disabling a user 

account's password ? 

 

Locking will prevent the user from logging on to the system with his password by putting a ! in front 

 

6. As root change the password of einstime to stargate. 

 

 

passwd einstime  

 

7. Now try changing the password of serena to serena as serena. 

 

Passwd serena 

 

8. Make sure every new user needs to change his password every 10 days. 

 

chage -M 10 serena 
 

 

 

9. Set the warning number of days to four for the kornuser. 

 

useradd -s /bin/ksh kornuser ; passwd kornuser 
 

 

10a. Set the password of two separate users to stargate. Look at the encrypted 

stargate's in /etc/shadow and explain. 

10b. Take a backup as root of /etc/shadow. Use vi to copy an encrypted stargate to 

another user. Can this other user now log on with stargate as a password ? 

 

11. Put a file in the skeleton directory and check whether it is copied to user's home 

directory. When is the skeleton directory copied ? 

 

When a new user's home directory is created, it will be a copy of /etc/skel  

 

12. Why use vipw instead of vi ? What could be the problem when using vi or vim ? 

 

 
 

vipw will give a warning when someone else is already using that file  

 

 

13. Use chsh to list all shells, and compare to cat /etc/shells. Change your login shell 

to the Korn shell, log out and back in. Now change back to bash. 

 

chsh -lcat /etc/shells 

 

 

14. Which useradd option allows you to name a home directory? 

 

sermod -d/home/newfolder 

 

15. How can you see whether the password of user harry is locked or unlocked? Give a solution with grep and a solution with passwd. 

 

 
grep serena /etc/shadow 
passwd -S serena 

 
 

 

 

16. Create the groups tennis, football and sports. 

 

groupadd tennis ; groupadd football ; groupadd sports 
 

 

17. In one command, make venus a member of tennis and sports. 

 

 

usermod -a -G tennis,sports venus 
 

 

18. Rename the football group to foot. 

 

groupmod -n foot football 
 

 

 

19. Use vi to add serena to the tennis group. 

 

vi /etc/group 
 

 

 

20. Use the id command to verify that serena is a member of tennis. 

 

Id exit serena 

Then log in serena  
