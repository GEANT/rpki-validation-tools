geant-ne-routinator
=========

This role installs Routinator (currently 0.6.2), an RPKI validator from NLNETlabs (https://www.nlnetlabs.nl/projects/rpki/routinator/).

The role copies an executables obtained following this procedure: https://github.com/NLnetLabs/routinator.

It also configure syslog and logrotate for routinator logs.


Requirements
------------
This role has been developed and tested on Ubuntu 18.04 (Bionic Beaver)
Firewalling should be in place allowing port 8282 in INPUT.

Role Variables
--------------
These are the variables in use: 
Defaults: 
* __routinator_home:__ /var/cache/routinator
* __routinator_loglevel:__ "WARN"

To be filled (in the hosts.yaml file): 
* __routinator_listen_ipv4__: 192.168.56.199:8282
* __routinator_listen_ipv6__:
* __routinator_syslog_destination:__ 
              __protocol:__ tcp 
              __target:__ 10.10.10.10
              __port:__ 514

Dependencies
------------
No dependencies

Example Playbook
----------------

Check install_routinator.yaml in the upper folder. 

License
-------

BSD

Author Information
------------------

simone.spinelli@geant.org
