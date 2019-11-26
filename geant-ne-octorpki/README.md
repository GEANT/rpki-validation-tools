geant-ne-octorpki 
=========

This role installs OctoRPKI and GoRTR on a Ubuntu 18.04.
It also configure rsyslog to manage the logging on a separate file and if needed to a syslogserver. 
OctoRPKI and GoRTR are run as systemd Services. 

For more info: 
https://github.com/cloudflare/cfrpki


Requirements
------------

This role has been developed and tested on Ubuntu 18.04 (Bionic Beaver)


Role Variables
--------------

In the hosts.yaml you can specifiy a syslog destination:

* __routinator_syslog_destination:__ 
              __protocol:__ tcp 
              __target:__ 10.10.10.10
              __port:__ 514

Dependencies
------------

NA

Example Playbook
----------------

Check install_octorpki.yaml in the upper folder. 



Author Information
------------------

simone.spinelli@geant.org
