Kryp7ik Galera
=========

This role will install a MariaDB Galera cluster on CentOS/RHEL 7 systems.

Requirements
------------

None

Role Variables
--------------
A mysql root user password must be set
```
galera_root_password: 'topsecret'
```
The group name from the inventory file must also be specified but defaults as the following
```
galera_cluster_inventory_group: 'galera_nodes'
```
By default this role will assume the first host in the inventory group will be the master node. Modify this variable to change that
```
galera_master_node: '{{ groups[galera_cluster_inventory_group][0] }}'
```
Other variables and their default values
```
galera_bind_address: 0.0.0.0
host_has_selinux: True
galera_cluster_name: 'galera_cluster'
```

Dependencies
------------

None

Example Playbook
----------------
```
- hosts: galera_nodes
  remote_user: USERNAME
  become: yes
  become_method: sudo
  vars_prompt:
    - name: galera_root_password
      prompt: 'Enter the desired mysql root users password'
      private: yes

  roles:
    - { role: galera }
```
License
-------

BSD

