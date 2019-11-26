# rpki-validation-tools
Ansible roles for deploying RPKI validators on Ubuntu

## General

This repository contains two Ansible playbooks, each defining a role to deploy an RPKI validator, either [Routinator 3000](https://github.com/NLnetLabs/routinator) or [Octo-RPKI](https://github.com/cloudflare/cfrpki) (and the associated go-rtr software). There is a common Inventory file, hosts.yaml which defines some parameters to suit the target environment. The playbooks been tested on Ubuntu 18.04.

What you will get:
- Routinator 3K and/or octo-rpki + go-rtr
- rsyslog and logrotate
- A systemd service to get things going
- Automatic installation of TALs

## Pre-requirements

To run these playbooks with little fuss, you will need:
- Ubuntu (we developed this on 18.04)
- git
- Ansible
- sshpass (if you want to use Ansible with passwords)

Git clone the repository to your ansible machine, cd into the directory 'rpki-validation-tools'..


## Configuring the inventory

The `hosts.yaml` file has all the things you need to edit up front. Here are some over-zealous comments!

```---
all:
  children: 
    routinator_vms:
      hosts:
        routinator-vm: ## define your intended routinator hosts
    octorpki_vms:
      hosts:
        octorpki-vm: ## define your intended octo-rpki hosts
  hosts:
    routinator-vm:
      ansible_host: 192.168.56.198 ## target host
      become: yes ## install as root
      ansible_python_interpreter: /usr/bin/python3
      ansible_user: vagrant ## the user ansible will run as
      routinator_listen_addresses:
        - 192.168.56.198 ## you can define v4 and/or v6 addresses
      routinator_syslog_destination:
              protocol: tcp
              target: 10.10.10.10
              port: 514
    octorpki-vm:
      ansible_host: 192.168.56.197
      become: yes
      ansible_python_interpreter: /usr/bin/python3
      ansible_user: vagrant
      octorpki_syslog_destination:
              protocol: tcp
              target: 192.168.22.23
              port: 666
```


## Running the playbooks

Once you have edited the inventory file to suit your environment, run the playbooks:

```ansible-playbook -i hosts.yaml install_routinator.yaml```

or with ssh/sudo passwords:

```ansible-playbook -i hosts.yaml install_routinator.yaml --ask-pass --ask-become-pass```

This will install Routinator. You can do the same for octo-rpki!

```ansible-playbook -i hosts.yaml install_octorpki.yaml```

And again, but this time with ssh/sudo passwords:

```ansible-playbook -i hosts.yaml install_octorpki.yaml --ask-pass --ask-become-pass```

## Validating the validators
The role will set up its validator as a systemd service, so you can check the status with `sudo systemctl status routinator` (or the octo-rpki equivalent). 

Connect your routing equipment to the RTR port (8282 by default) and begin validating your routes!

