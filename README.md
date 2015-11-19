# Ansible Corosync
Install Corosync on CentOS 7 and Debian 8 Jessie distributions.

This role supports protocols:
- Multicast (udp)
- Unicast (udpu)

Because the version 1 of Coroync is "not supported" anymore, this module provides only a support for the version 2 of Corosync.

## Requirements
None.

## Role Variables
The description of all options is available here: http://manpages.ubuntu.com/manpages/wily/man5/corosync.conf.5.html
```
    corosync_crypto_cipher | default('aes256')
    corosync_crypto_hash | default('sha256')
    corosync_rrp_mode
    corosync_netmtu | default(1500)
    corosync_vsftype | default('ykb')
    corosync_transport
    corosync_cluster_name | default('uoi')
    corosync_config_version
    corosync_ip_version | default('ipv4')
    corosync_token | default(1000)
    corosync_token_retransmit
    corosync_hold
    corosync_token_retransmits_before_loss_const
    corosync_join
    corosync_send_join
    corosync_consensus
    corosync_merge
    corosync_downcheck
    corosync_fail_recv_const
    corosync_seqno_unchanged_const
    corosync_heartbeat_failures_allowed
    corosync_max_network_delay
    corosync_window_size
    corosync_max_messages
    corosync_miss_count_const
    corosync_rrp_problem_count_timeout
    corosync_rrp_problem_count_threshold
    corosync_rrp_problem_count_mcast_threshold
    corosync_rrp_token_expired_timeout
    corosync_rrp_autorecovery_check_timeout
    corosync_provider | default('corosync_votequorum')
    corosync_expected_votes
    corosync_timestamp | default ('off')
    corosync_fileline | default('off')
    corosync_to_stderr | default('on')
    corosync_to_logfile | default('off')
    corosync_to_syslog | default('on')
    corosync_logfile
    corosync_logfile_priority | default('info')
    corosync_syslog_facility | default('daemon')
    corosync_syslog_priority | default('info')
    corosync_debug | default('off')
    corosync_subsys | default('QUORUM')
    corosync_subsys_debug | default('off')
    corosync_subsys_tags
    corosync_ipc_type | default('native')
```

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