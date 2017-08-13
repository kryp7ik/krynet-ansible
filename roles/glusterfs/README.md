Kryp7ik Gluster Cluster
=========

Installs GlusterFS on multiple hosts and creates a volume.  Designed for CentOS / RHEL 7

Requirements
------------

None

Role Variables
--------------

    # centos-release-gluster310 : Gluster 3.10 (Long Term Stable) packages from the CentOS Storage SIG
    # centos-release-gluster36 : GlusterFS 3.6 packages from the CentOS Storage SIG repository
    # centos-release-gluster37 : GlusterFS 3.7 packages from the CentOS Storage SIG repository
    # centos-release-gluster38 : GlusterFS 3.8 packages from the CentOS Storage SIG repository
    # centos-release-gluster39 : Gluster 3.9 (Short Term Stable) packages from the CentOS Storage SIG
    
    gluster_release_package: 'centos-release-gluster310'
    
    gluster_firewall_ports:
      - '24007-24009/tcp'
      - '49152-49160/tcp'
      - '38465-38467/tcp'
      - '111/tcp'
      - '111/udp'
      - '2049/tcp'
    
    gluster_volume_name: 'share'
    
    gluster_bricks:
      - '/glusterfs/brick1'
    
    gluster_rebalance: yes
    
    # Either specify an inventory group or create a list of hosts
    gluster_cluster_nodes: '{{ groups.gluster_cluster }}'

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: glusterfs }

License
-------

BSD
