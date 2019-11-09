ssh_admin_key_service
=====================

An ansible role to deploy and secure an ssh key from root user

Requirements
------------

* SElinux in enforcing mode
* systemd --user enabled
* polkit
* an ssh key in role file ***files/id_rsa***

Role Variables
--------------

* ssh_admin_key_service_allow_group: "wheel", the default group allowed to 
* ssh_admin_key_service_name: "ssh_add_root", name of the systemd main service
* ssh_admin_key_service_keypath: "/root/.ssh/id_rsa_root", remote ssh key file location

Usage
-----

```
# create user's agent
systemctl --user start ssh_user_agent.service
# set the socket path in your environement
export SSH_AUTH_SOCK="/tmp/ssh-agent.$(whoami).socket"
# finally *** as regular user *** load the private key to your ssh-agent 
systemctl start "ssh_add_root@$(whoami).service"
ssh-add -l
# 4096 SHA256:cbHy59r0xtkKbrZy3KmwbS980h7MYKZ2BHyBPKz+gas test daemon (RSA)
```

Dependencies
------------

N/A

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: ssh_admin_key_service }

License
-------

BSD


