Kryp7ik Filebeat
=========

This role will install and configure Filebeat on CentOS / RHEL 7 hosts.

Requirements
------------

Should have an ELK server installed so filebeat can be configured to communicate with it.

Hosts should have rsync installed in order to retrieve the ssl cert from the ELK server.

Role Variables
--------------

    # hostname of the elk server
    elk_server: 'elk.krynet.com'
    
    # path of the ssl cert on the remote elk server
    elk_ssl_cert_remote_path: '/etc/pki/tls/certs/logstash-forwarder.crt'
    
    # path to place the ssl cert on the local host
    elk_ssl_cert_local_path: '/etc/pki/tls/certs/logstash-forwarder.crt'
    
    # filebeat configuration option of where to retrieve log files
    filebeat_log_path: '/var/log/*.log'

Dependencies
------------

None

Example Playbook
----------------

    - hosts: elk_beats
      remote_user: username
      become: yes
      become_method: sudo
      roles:
        - { role: filebeat, tags: 'filebeat' }

License
-------

BSD
