ansible-vsftpd
==============

Install FTP server - [vsftpd](https://security.appspot.com/vsftpd.html).


Synopsis
--------

  - Install vsftpd
  - Usage virtual users ([libpam-pwdfile](https://github.com/tiwe-de/libpam-pwdfile))
  - Support TLS. Default is enabled only security connections.
  - Create the test user (default is disable):
    - login: k0st1an
    - password: 42


Tested
------

  - Debian Jessie
  - Ansible v1.9.1


Role Variables
--------------

See `vars/main.yml` for standard options:

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

    pwd_file: /etc/vsftpd

    test_user_is_enable: no
    test_user: k0st1an
    test_user_password: 42

Documentation of the [vsftpd](https://security.appspot.com/vsftpd/vsftpd_conf.html).


License
-------

MIT


Author Information
------------------

GitHub: https://github.com/k0st1an

Author: Konstantin Kruglov

Contact: kruglovk@gmain.com


Cli command
-----------

There is a script `vsftpd-users` installed into `/sbin/`. It can add, delete, update, and display
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
