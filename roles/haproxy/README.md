Kryp7ik HAProxy
=========

This role will install HAProxy as a webserver or Galera cluster load balancer on a CentOS/RHEL 7 host.

Requirements
------------

You must have an inventory group for your webservers and/or galera nodes of which HAProxy will load balance.

Role Variables
--------------
Most importantly of these variables is to ensure the ha_webserver_inventory_group and ha_galera_inventory_group are set
to your specefic host group names.

    enable_ha_stats: True
    ha_stats_user: 'username'
    ha_stats_password: 'Password!'
    ha_stats_bind_port: 8080
    
    # Configuration options for HAProxy when being configured for webservers
    ha_webserver_front_bind_addr: '*'
    ha_webserver_front_bind_port: 80
    ha_webserver_backend_port: 80
    
    # Optionally bind to port 443 also
    ha_webserver_ssl: True
    ha_webserver_ssl_front_port: 443
    ha_webserver_ssl_cert_path: '/etc/haproxy/certs/cert.pem'
    
    # Group name of the webservers in your inventory
    ha_webserver_inventory_group: 'webservers'
    
    #
    # Configuration options for HAProxy when being configured for Galera cluster
    #
    # Binding frontend to the hosts internal ip
    ha_galera_frontend_addr: '{{ hostvars[inventory_hostname]["ansible_eth0"]["ipv4"]["address"] }}'
    ha_galera_frontend_port: 3030
    ha_galera_backend_port: 3306
    ha_galera_check_port: 9200
    
    # Group name of the galera hosts in your inventory
    ha_galera_inventory_group: 'galera_nodes'

Dependencies
------------

None

Example Playbook
----------------

Example inventory file...
```
[webservers]
web01.krynet.com
web02.krynet.com

[galera_nodes]
galera01.krynet.com
galera02.krynet.com
galera03.krynet.com
    
[lb]
web-haproxy.krynet.com hap_role:'webserver'
galera-haproxy.krynet.com hap_role:'galera'
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

