Role Name: os-bootstrap
=======================

[![Build Status](https://travis-ci.org/ichundu/ansible-role-os-bootstrap.svg?branch=master)](https://travis-ci.org/ichundu/ansible-role-os-bootstrap.svg?branch=master)

Bootstrap OS after server provisioning.

Requirements
------------

None.

Role Variables
--------------

- Default variables in `defaults/main.yml`:

  | Name		  | Default value		  | Description	     	|
  |-----------|-------------------|-------------------|
  | `reboot` | `False` | Whether to reboot instance after setup or not |
  | `osbootstrap_epel` | `True` | Whether to enable the EPEL repository |
  | `osbootstrap_epel_url` | `https://dl.fedoraproject.org/pub/epel/epel-release-latest-{{ ansible_distribution_major_version }}.noarch.rpm` | EPEL release rpm package url |
  | `osbootstrap_epel_repo` | `{{ osbootstrap_epel_url if ansible_distribution == 'RedHat' else 'epel-release' }}` | EPEL release package name, on CentOS `epel-release` is installed, on RedHat the package from the provided URL is installed instead |
  | `osbootstrap_packages` | `[]` | Packages to install after provisioning, this is an OS-specific vairable and is included dynamically dpending on the distro from the `vars/` directory |
  | `osbootstrap_selinux` | `[ {'policy: targeted', 'state: permissive'} ]` | SELinux default state |
  | `ec2_bootstrap_packages` | `[ libselinux-python, libsemanage-python, vim, htop, bash-completion, rng-tools ]` | Basic packages that should be installed on every new instance |
  | `osbootstrap_timezone` | `[]` | Timezone region |
  | `osbootstrap_host` | `inventory_hostname` | IP address of target host used in wait_for task |

- OS-specific variables are included dynamically vial the [include_vars](https://docs.ansible.com/ansible/include_vars_module.html) module:

  ```yaml
  - name: Include OS-specific variables
    include_vars: "{{ item }}"
    with_first_found:
      - "{{ ansible_os_family }}.yml"
      - "{{ ansible_distribution }}.yml"
  ```

  ...which includes either `RedHat.yml` or `Ubuntu.yml` file inside the `vars/` directory.

- We also use `set_fact` task to establish whether packages that require reboot have been updated.

  ```yaml
  - name: EL6 | Check if reboot is required
    set_fact:
      reboot_required: true
    when: "'kernel.' or 'kernel-firmware' or 'glibc.' 'hal.' in item"
    with_items: "{{ yum_result.results }}"
  ```

Dependencies
------------

None.

Example Playbook
----------------

```yaml
    - hosts: servers
      roles:
         - ichundu.os-bootstrap
```

License
-------

GPLv2

Author Information
------------------

https://github.com/ichundu
