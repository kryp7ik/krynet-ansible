Kryp7ik PHP7
=========

This role will install PHP 7 on a CentOS/RHEL 7 host.

Requirements
------------

None

Role Variables
--------------

---
    # php version to install
    php_version: "71w"
    
    # php.ini options
    php_allow_url_fopen: "On"
    php_timezone: "America/Detroit"
    php_disable_functions: "exec,passthru,shell_exec,system,proc_open,popen"
    php_display_errors: "Off"
    debug_mode: false
    php_error_reporting: "E_ALL & ~E_DEPRECATED & ~E_STRICT"
    php_memory_limit: "1024M"
    php_opcache_enable: 1
    php_opcache_revalidate_freq: 0
    php_post_max_size: "20M"
    php_serialize_precision: 17
    php_session_cookie_httponly: 1
    php_session_use_strict_mode: 1
    php_soap_wsdl_cache_dir: '/php/cache/wsdl'
    php_upload_max_filesize: "20M"
    php_upload_tmp_dir: "/php/cache/upload_tmp"
    
    # packages to install
    php_packages:
      - 'php{{ php_version }}-cli'
      - 'php{{ php_version }}-common'
      - 'php{{ php_version }}-fpm'
      - 'php{{ php_version }}-gd'
      - 'php{{ php_version }}-mysqlnd'
      - 'php{{ php_version }}-opcache'
      - 'php{{ php_version }}-pdo'
      - 'php{{ php_version }}-mcrypt'
    
    # php_allow_url_fopen must be set to 'on' for composer installation
    install_composer: true

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
