# Ansible Corosync
Install Corosync on CentOS 7 and Debian 8 Jessie distributions.

This role supports protocols:
- Multicast (udp)
- Unicast (udpu)

Because the version 1 of Coroync is "not supported" anymore, this module provides only a support for the version 2 of Corosync.

## Requirements
None.

## Role Variables
A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

## Dependencies
None.

## Example Playbook
The following example will create a Corosync cluster using multicast, if multicast is used you have to define the expected_votes (3 for three nodes). If you want to configure firewalld rules, be sure that corosync_firewalld is set to true
### Multicast (1 ring)
```
---
corosync_firewalld: true
corosync_expected_votes: 3

corosync_interfaces:
  - bindnetaddr: 192.168.56.0
    mcastaddr: 226.94.1.1
    mcastport: 5405
    ttl: 1
```

The following example will create a Corosync cluster using multicast with two rings.
### Multicast (2 rings)
```
---
corosync_firewalld: true
corosync_expected_votes: 3

corosync_interfaces:
  - bindnetaddr: 192.168.56.0
    mcastaddr: 226.94.1.1
    mcastport: 5405
    ttl: 1
  - bindnetaddr: 10.14.130.0
    mcastaddr: 227.94.1.1
    mcastport: 5407
    ttl: 100
```
The following example will create a Corosync cluster using unicast with two rings, if unicast is used you have to define the corosync_transport: udpu and define corosync_node_list as an array.
### Unicast
```
---
corosync_firewalld: true
corosync_node_list: ['ctrl01', 'ctrl02', 'ctrl03']
corosync_transport: 'udpu'

corosync_interfaces:
  - bindnetaddr: 192.168.56.0
    mcastaddr: 226.94.1.1
    ttl: 20
    members:
      - 226.94.1.10
      - 226.94.1.11
      - 226.94.1.12
  - bindnetaddr: 10.14.130.0
    mcastaddr: 227.94.1.1
    ttl: 100
    members:
      - 227.94.1.10
      - 227.94.1.11
      - 227.94.1.12
```

## License
BSD

## Author Information
This role was created in 2015 by Gaëtan Trellu (goldyfruit).