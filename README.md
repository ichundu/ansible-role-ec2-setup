Role Name: ec2-setup
====================

Initial basic configuration after provisioning an ec2 instance.

Requirements
------------

None.

Role Variables
--------------

Default variables:

| Name		| Default value		| Description		|
|-----------|-------------------|-------------------|
| `ec2_setup_python` | `[ libselinux-python, libsemanage-python ]` | Selinux python libraries |
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
