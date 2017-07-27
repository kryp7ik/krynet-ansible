Kryp7ik ipa-server
=========

This role will install a full IPA server with DNS on a CentOS/RHEL 7 host

Requirements
------------

Ensure that you set the hostname on the host to match the domain that you will be configuring the DNS for.
For example if the domain is krynet.com set the hostname to ipa.krynet.com

Role Variables
--------------
    
    ipa_domain: 'ipa.krynet.com'
    ipa_realm: 'IPA.KRYNET.COM'
    ipa_dns_forward: '8.8.8.8'
    
    # Specify the number to start incrementing uid's from
    ipa_id_start: 3000
    
    # The admin password
    ipa_admin_pass: 'secret'
    
    # The admin directory manager password
    ipa_dm_pass: 'anothersecret'

Dependencies
------------

None

Example Playbook
----------------

    - hosts: ipa-server
      remote_user: USERNAME
      become: yes
      become_method: sudo
      vars_prompt:
        - name: ipa_admin_pass
          prompt: 'Please type in the admin password'
    
        - name: ipa_dm_pass
          prompt: 'Please type in the admin directory manager password'
      roles:
        - { role: ipa-server, tags: 'ipa-server' }

License
-------

BSD

