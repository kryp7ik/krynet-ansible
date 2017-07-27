Kryp7ik ipa-client
=========

This role is designed to enroll hosts running CentOS/RHEL 7 with a FreeIPA server

Requirements
------------

Must have an active FreeIPA server with DNS along with credentials to authenticate the host
with the IPA server.

Role Variables
--------------

    ipa_server: 'ipa.krynet.com'
    ipa_domain: 'krynet.com'
    ipa_realm: 'IPA.KRYNET.COM'

Dependencies
------------

None

Example Playbook
----------------
_The hostname should be set on the hosts (prior to running the playbook) to match your domain because this playbook uses the hostname
to create the DNS entry on the ipa server._

Given the host(s) you are enrolling most likely do not have DNS records at this point I recommend running this playbook
by it self and specifying the host(s) via the -i flag...

    $ ansible-playbook -K -i 192.168.1.10,192.168.1.11 ipa-client-playbook.yml

ipa-client-playbook.yml
```
- hosts: all
  remote_user: USERNAME
  become: yes
  become_method: sudo
  vars_prompt:
    - name: ipa_principal
      prompt: 'Enrollment username (principal)'
      private: no

    - name: ipa_principal_pass
      prompt: 'Enrollment user password'
  roles:
    - { role: ipa-client, tags: 'ipa-client' }
```

License
-------

BSD

