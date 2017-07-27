Kryp7ik HAProxy
=========

This role will install HAProxy as a webserver load balancer on a CentOS/RHEL 7 host.

Requirements
------------

Assumes you have an inventory group named 'webservers' containing the hosts to direct traffic to.

Role Variables
--------------

    enable_ha_stats: true
    ha_stats_user: 'myuser'
    ha_stats_password: 'secretpass'
    ha_stats_bind_port: 8080
    
    ha_front_bind_addr: '*'
    ha_front_bind_port: 80

Dependencies
------------

None

Example Playbook
----------------
Again this role assumes you have an inventory group called 'webservers' containing the hosts to direct traffic to.

Example inventory file...
```
[webservers]
web01.krynet.com
web02.krynet.com
    
[lb]
haproxy.krynet.com
```
Playbook Example

    - hosts: lb
      remote_user: USERNAME
      become: yes
      become_method: sudo
      roles:
        - { role: haproxy, tags: 'haproxy' }

License
-------

BSD

