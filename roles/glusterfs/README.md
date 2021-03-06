Kryp7ik Gluster Cluster & Ganesha
=========

Installs GlusterFS on multiple hosts and creates a volume.  Designed for CentOS / RHEL 7.
Working on NFS Ganesha but it is not completed yet.

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
    
    gluster_volume_name: 'share'
    
    # It is advisable that your gluster share is using a different disk or partition than the root filesystem
    # This role will not create or mount any disks.
    gluster_bricks:
      - '/mnt/glusterfs/brick1'
    
    gluster_rebalance: yes
    
    # Specify number of nodes that should replicate data
    gluster_replicas: 2
    
    # If using the root partition you will need to set this to yes
    gluster_force: no
    
    # Either specify an inventory group or create a list of hosts
    gluster_cluster_nodes: '{{ groups.gluster_cluster }}'
    
    
    # ----------------- NFS Ganesha -------------------------------------------
    # This part of the role is not completed yet
    install_ganesha: False
    
    ganesha_ha_name: 'ganesha-ha-360'
    # The HA_CLUSTER_NODES will be set to the nodes defined above in the gluster_cluster_nodes variable


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
