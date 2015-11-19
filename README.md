Ansible Role: Corosync
=========

Install Corosync on CentOS 7 and Debian 8 Jessie distributions.

The role supports protocols:
- Multicast
- Unicast 

Only the version 2 of Corosync is supported by this role.

Requirements
------------

None.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

This role was created in 2015 by Gaëtan Trellu (goldyfruit).