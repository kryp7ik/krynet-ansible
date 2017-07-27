Kryp7ik Nginx
=========

Install & Configure nginx web server on CentOS/RHEL 7 hosts

Requirements
------------

None

Role Variables
--------------

    # If SELinux is enabled on the host change boolean to allow remote db connect
    selinux_remote_db: true
    open_http_ports_firewalld: true
    
    # Setting this to true will create the default site with the following parameters
    nginx_create_default_site: false
    nginx_port: 80
    nginx_root: /var/www/html
    nginx_index: index.html
    
    # Specify list of servers to create basic PHP vhosts for or 'none'
    nginx_php_sites: 'none'
    #  - server:
    #      domain: 'krynet.com'
    #      listen: '80'
    #      root: '/var/www/kryp7ik'
    #      public_folder: 'public'
    #      index_files: 'index index.html index.htm index.php'
    #      access_log: 'off'
    #      error_log_path: '/var/log/nginx/kryp7ik-error.log'

Dependencies
------------

'base' role found in this repository or manually install the following packages

    $ yum install epel-release policycoreutils-python libselinux-python libsemanage-python


Example Playbook
----------------

    - hosts: webservers
      remote_user: kryptik
      become: yes
      become_method: sudo
      roles:
        - { role: base, tags: 'base' }
        - { role: php7, tags: 'php7' }
        - { role: nginx, tags: 'nginx' }

License
-------

BSD
