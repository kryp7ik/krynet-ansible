Kryp7ik ELK
=========

This role will install Elastic Stack (ELK / Elastic Search, Logstash, Kibana) on a CentOS / RHEL 7 host.

Requirements
------------

None

Role Variables
--------------

    java_package: 'java-1.8.0-openjdk.x86_64'
    
    # Logstash
    logstash_ssl_key: '/etc/pki/tls/private/logstash-forwarder.key'
    logstash_ssl_crt: '/etc/pki/tls/certs/logstash-forwarder.crt'

Dependencies
------------

None

Example Playbook
----------------

    - hosts: elk
      remote_user: username
      become: yes
      become_method: sudo
      roles:
        - { role: elk, tags: 'elk' }

License
-------

BSD
