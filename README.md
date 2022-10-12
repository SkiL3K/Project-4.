Practice: Users and Groups

1. Create the users Serena Williams, Venus Williams and Justine Henin, all of them
with password set to stargate, with username (lower case!) as their first name, and
their full name in the comment. Verify that the users and their home directory are
properly created. –
sudo su; useradd -c "Serena Williams" Serena; useradd -c "Venus Williams" Venus; useradd -c "Justine Henin" Justine; passwd Serena; passwd Venus; passwd Justine

2. Create a user called kornuser, give him the Korn shell (/bin/ksh) as his default
shell. Log on with this user (on a command line or in a tty). -
sudo useradd -m -d /bin/ksh/Korn kornuser; su kornuser

3. Create a user named einstime without home directory, give him /bin/date as his
default logon shell. What happens when you log on with this user ? Can you think of
a useful real world example for changing a user's login shell to an application ?
sudo useradd -s /bin/date einstime

4. Try the commands who, whoami, who am i, w, id, echo $USER $UID .

5a. Lock the venus user account with usermod.- sudo usermod -L Venus

5b. Use passwd -d to disable the serena password. Verify the serena line in /etc/
shadow before and after disabling. –
before disabling - Serena:$y$j9T$EVz2SIDduL9hvdcT8vzzV1$K/j/jB3DY.tXgOtErYjuMLoIuYkrncElKRMMsqSfVo9:19271:0:99999:7:::
sudo passwd -d Serena
after disabling - Serena::19271:0:99999:7:::

5c. What is the difference between locking a user account and disabling a user
account's password ? 
One can disable an account in several ways:  replace the password field with "x", set to 0 the day in /etc/shadow that indicates the password has expired, replace the user's shell with /bin/false or a custom program which does not allow the user to do anything useful and is not in /etc/shells (4) remove the passwd (or shadow or both) entry for that user.

6. As root change the password of einstime to stargate.
sudo su; passwd einstime
new password: stargate

7. Now try changing the password of serena to serena as serena.
su Serena
Password:stargate
$ passwd
Current password:stargate
New password:serena
BAD PASSWORD: The password is shorter than 8 characters


8. Make sure every new user needs to change his password every 10 days.
sudo chage -E 10 (username)

9. Set the warning number of days to four for the kornuser.
sudo chage -W 4 kornuser

10a. Set the password of two separate users to stargate. Look at the encrypted
stargate's in /etc/shadow and explain.
/etc/shadow is a text file that contains information about the system's users' passwords. If you used passwd, then the salt will be different for the two encrypted passwords.

10b. Take a backup as root of /etc/shadow. Use vi to copy an encrypted stargate to
another user. Can this other user now log on with stargate as a password ?
Yes the other user can log on with stargate password.

11. Put a file in the skeleton directory and check whether it is copied to user's home
directory. When is the skeleton directory copied ?
The /etc/skel directory contains files and directories that are automatically copied over to a new user's directories.

12. Why use vipw instead of vi ? What could be the problem when using vi or vim ?
vipw will give a warning when someone else is already using that file.

13. Use chsh to list all shells, and compare to cat /etc/shells. Change your login shell
to the Korn shell, log out and back in. Now change back to bash.
cat /etc/shells
chsh -s /bin/ksh/Korn kornuser
chsh -s /bin/bash kornuser

14. Which useradd option allows you to name a home directory ?
sudo useradd -m -d

15. How can you see whether the password of user harry is locked or unlocked ? Give a solution with grep and a solution with passwd.
grep harry /etc/shadow
passwd -S harry

16. Create the groups tennis, football and sports.
groupadd tennis ; groupadd football ; groupadd sports

17. In one command, make venus a member of tennis and sports.
sudo usermod -a -G tennis,sports venus

18. Rename the football group to foot.
sudo usermod -n foot football
 
19. Use vi to add serena to the tennis group.
vi /etc/group

20. Use the id command to verify that serena is a member of tennis.
id serena
after logoff logon serena is a member of tennis

