Role Name
=========

This role installs OctoRPKI and GoRTR on a Ubuntu 18.04.
It also configure rsyslog to manage the logging on a separate file and if needed to a syslogserver. 
OctoRPKI and GoRTR are run as systemd Services. 

For more info: 
https://github.com/cloudflare/cfrpki


Requirements
------------

NA

Role Variables
--------------

Variables that should be filled are:

* octorpki_homedir (default /usr/share/octorpki)

Dependencies
------------

NA

Example Playbook
----------------

NA

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
