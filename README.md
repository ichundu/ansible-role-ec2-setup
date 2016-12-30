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
| `epel_repo` | `https://dl.fedoraproject.org/pub/epel/epel-release-latest-{{ ansible_distribution_major_version }}.noarch.rpm` | Epel repository rpm url, substitute with `epel-release` on CentOS systems |
| `epel_rpm_gpg` | `/etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-{{ ansible_distribution_major_version }}` | Epel rpm GPG key to import |

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
