# ansible-vsftpd

# Status

Developing.


# Tested

  - Debian Jessie
  - Ansible v1.9.1


# Synopsis

  - Install [vsftpd](https://security.appspot.com/vsftpd.html)
  - Usage virtual users ([libpam-pwdfile](https://github.com/tiwe-de/libpam-pwdfile))
  - Create the test user (optional):
    - login: k0st1an
    - password: 42


# Vars

See `group_vars/ftp` for standard options:

    # vsftpd settings
    vsftpd_ftpd_banner: Welcome to FTP
    vsftpd_max_per_ip: 100
    vsftpd_pasv_min_port: 10000
    vsftpd_pasv_max_port: 14000
    vsftpd_xferlog_enable: 'YES'
    vsftpd_local_root: /srv/ftp
    vsftpd_ssl_enable: 'YES'
    vsftpd_tls_only: 'YES'
    vsftpd_user_config_dir: /etc/vsftpd.d
    # end vsftpd settings

    vsftpd_pwd_file: /etc/vsftpd

    test_user_is_enable: no
    test_user: k0st1an
    test_user_password: 42

Documentation of the [vsftpd](https://security.appspot.com/vsftpd/vsftpd_conf.html).

# Usage

```
ansible-playbook -i hosts vsftpd.yml
```

or below, if you do not want to create a test user:

```
ansible-playbook -i hosts vsftpd.yml --skip-tags=testuser
```

Adding new user:

```
ansible-playbook -i hosts vsftpd-user.yml -t add
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
  User DB: /etc/vsftpd
  Local root: /srv/ftp/    # Where will be create directory of the user
```

# Version

  - 0.3
