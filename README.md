Role Name: ec2-setup
====================

Initial basic setup after provisioning an ec2 instance.

Requirements
------------

None.

Role Variables
--------------

Default variables:

| Name		| Default value		| Description		|
|-----------|-------------------|-------------------|
| `rebootrequired` | `False` | Whether to reboot instance after setup or not |
| `ec2_setup_epel` | `True` | Whether to enable the EPEL repository |
| `ec2_setup_packages` | `[ libselinux-python, libsemanage-python, vim, htop, bash-completion, rng-tools ]` | Basic packages that should be installed on every new instance |
| `ec2_setup_timezone` | `Europe/Berlin` | System timezone |

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: ec2-setup, ec2_timezone: "Europe/Amsterdam" }

License
-------

GPLv2

Author Information
------------------

https://github.com/ichundu
