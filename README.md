# ansible-vsftpd

# Status

Developing.


# Tested

  - Debian Jessie
  - Ansible v1.9.1


# Synopsis

  - Install [vsftpd](https://security.appspot.com/vsftpd.html)
  - Usage virtual users ([libpam-pwdfile](https://github.com/tiwe-de/libpam-pwdfile))
  - Create the test user:
    - login: k0st1an
    - password: 42


# Usage

```
ansible-playbook -i hosts vsftpd.yml --ask-pass --ask-become-pass
```

or below, if you do not want to create a test user:

```
ansible-playbook -i hosts vsftpd.yml --ask-pass --ask-become-pass --skip-tags=testuser
```

Adding new user:

```
ansible-playbook -i hosts vsftpd-user.yml --ask-pass --ask-become-pass -t add
```

This is playbook used script `vsftpd-users` on the remote machine, see below.


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

# Version

  - 0.2
