Kryp7ik Dokuwiki
=========

This role will install Dokuwiki on a CentOS/RHEL 7 host(s).

Requirements
------------

Host must have Nginx and PHP installed

Role Variables
--------------
The following are all the variables and their default values

Paths & Resources
```
dokuwiki_source: 'https://download.dokuwiki.org/src/dokuwiki/dokuwiki-stable.tgz'
root_folder: '/var/www/dokuwiki'
```

Configuration options for nginx server block
```
index_file: 'doku.php'
wiki_domain: 'wiki.mydomain.com'
max_upload_file_size: '4M'
ssl_cert: '/etc/ssl/certs/dokuwiki.crt'
ssl_key: '/etc/ssl/private/dokuwiki.key'
```
Ownership (the webserver_user and group must be set according to the Nginx install these variables have no impact on the nginx role)
```
dokuwiki_user: 'dokuwiki'
dokuwiki_group: 'dokuwiki'
webserver_user: 'nginx'
webserver_group: 'nginx'
```

Dependencies
------------

Either install Nginx & PHP manually or use the roles contained in this repo (nginx, php7)

Example Playbook
----------------

This is an example playbook using the roles in this repo


    - hosts: webservers
      remote_user: USERNAME
      become: yes
      become_method: sudo
      roles:
        - { role: base, tags: 'base' }
        - { role: php7, tags: 'php7' }
        - { role: nginx, tags: 'nginx' }
        - { role: dokuwiki, tags: 'dokuwiki' }

License
-------

BSD


