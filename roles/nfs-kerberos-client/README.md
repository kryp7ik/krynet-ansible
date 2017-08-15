Kryp7ik NFS Kerberos Client
=========

Installs and configures NFS automount with Kerberos authentication on CentOS / RHEL 7 hosts within an IPA managed network.

Requirements
------------

You will need to create the automount maps on the IPA server.

Role Variables
--------------

    # Keytab variables
    ipa_principal: 'admin'
    ipa_password: 'changeme'

Dependencies
------------

None

Example Playbook
----------------


    - hosts: servers
      roles:
         - { role: nfs-kerberos-client }

License
-------

BSD
