Kryp7ik NFS Kerberos Server
=========

Installs and configures a NFS server with Kerberos authentication on CentOS / RHEL 7 hosts within an IPA managed network.

Requirements
------------

You will need to create the folders/volumes that you want NFS to export.

Role Variables
--------------

    # Keytab variables
    # These two values are only used to authenticate with IPA to get the nfs keytab
    ipa_principal: 'admin'
    ipa_password: 'changeme'
    
    nfs_service_principal: 'nfs/nfs.krynet.com'
    keytab_location: '/etc/krb5.keytab'
    
    
    # NFS Variables
    nfs_exports:
      - '/mnt/nfs/home   192.168.1.0/24(rw,sec=krb5:krb5i:krb5p)'
      - '/mnt/nfs/share  192.168.1.0/24(rw,sec=krb5:krb5i:krb5p)'

Dependencies
------------

None

Example Playbook
----------------


    - hosts: servers
      roles:
         - { role: nfs-kerberos }

License
-------

BSD