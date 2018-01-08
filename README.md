ansible-vsftpd
==============

[![galaxy](https://img.shields.io/badge/galaxy-k0st1an.vsftpd-brightgreen.svg)](https://galaxy.ansible.com/detail#/role/6384)

Install FTP server - [vsftpd](https://security.appspot.com/vsftpd.html).


Synopsis
--------

  - Installs vsftpd
  - Allows use of virtual users ([libpam-pwdfile](https://github.com/tiwe-de/libpam-pwdfile))
  - Support TLS. Default is enabled i.e. only allow secure connections
  - Can create a list of users by setting the following variable:

```yaml
    vsftpd_users:
      - username: k0st1an
        password: 42
        state: present
      - username: johndoe
        password: pa55w0rd
        bindpath:
          - path: "/var/www/vhosts/example.com"
            owner: www-data
            group: www-data
          - path: "/var/www/vhosts/example.net"
      - username: janedoe
        state: absent
```

Tested
------

  - Debian Jessie
  - Ansible v1.9.1


Role Variables
--------------

See `vars/main.yml` for standard options:

```yaml
    ### vsftpd.conf settings
    
    vsftpd_ftpd_banner: Welcome to FTP
    vsftpd_max_per_ip: 100
    vsftpd_pasv_min_port: 10000
    vsftpd_pasv_max_port: 14000
    vsftpd_xferlog_enable: 'YES'
    vsftpd_local_root: /srv/ftp
    vsftpd_ssl_enable: 'YES'
    vsftpd_tls_only: 'YES'
    vsftpd_user_config_dir: /etc/vsftpd.d
    vsftpd_rsa_cert_file: /etc/ssl/certs/ssl-cert-snakeoil.pem
    vsftpd_rsa_private_key_file: /etc/ssl/private/ssl-cert-snakeoil.key
    vsftpd_write_enable: 'YES'
    vsftpd_pasv_enable: 'YES'
    vsftpd_chmod_enable: 'YES'
    vsftpd_file_open_mode: '0666'
    vsftpd_local_umask: '0022'
    vsftpd_utf8_filesystem: 'YES'
    vsftpd_users: []
    
    # Optionally enable chown on uploaded files. WARNING! 
    # continue only if you are aware of the security implications!
    #vsftpd_chown_uploads: 'YES'
    #vsftpd_chown_username: 'www-data'
    
    ### end vsftpd.conf settings

    vsftpd_pwd_file: /etc/vsftpd

    vsftpd_test_user_is_enable: no
    vsftpd_test_user: k0st1an
    vsftpd_test_user_password: 42
```

Additionally you can optionally set:

```yaml
    vsftpd_pasv_address: 52.17.204.30
    vsftpd_pasv_addr_resolve: NO
```

[vsftpd](https://security.appspot.com/vsftpd/vsftpd_conf.html) documentation.


License
-------

MIT


Author Information
------------------

GitHub: https://github.com/k0st1an

Author: Konstantin Kruglov

Contact: kruglovk@gmail.com


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
