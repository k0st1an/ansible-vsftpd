# ansible-vsftpd


# Installing vsftpd

```
ansible-playbook -i hosts vsftpd.yml --ask-pass --ask-become-pass
```

Will be installed:
  - [vsftpd](https://security.appspot.com/vsftpd.html)
  - [libpam-pwdfile](https://github.com/tiwe-de/libpam-pwdfile)


# Adding new user

```
ansible-playbook -i hosts vsftpd-user.yml --ask-pass --ask-become-pass -t add
```

This is playbook used script `vsftpd-users`, see below.


# Cli command

There is a script `/sbin/vsftpd-users`. It can add, delete, update, and display
a list of users.

```
$ /sbin/vsftpd-user

Usage vsftpd-user:
  add     <user name> <password> [<path to db file>]  # Add new user
  upgrade <user name> <password> [<path to db file>]  # Upgrade password of the user
  del     <user name> [<path to db file>]             # Delete the user
  list    [<path to db file>]                         # Show users

Predefined variable:
  User DB: /etc/vsftpd/ftp_users.db
  Local root: /srv/ftp
```
