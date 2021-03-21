# [ansible](#ansible)

Install and configure ansible on your system.

|GitHub|GitLab|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![github](https://github.com/robertdebock/ansible-role-ansible/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-ansible/actions)|[![gitlab](https://gitlab.com/robertdebock/ansible-role-ansible/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-ansible)|[![quality](https://img.shields.io/ansible/quality/35944)](https://galaxy.ansible.com/robertdebock/ansible)|[![downloads](https://img.shields.io/ansible/role/d/35944)](https://galaxy.ansible.com/robertdebock/ansible)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-ansible.svg)](https://github.com/robertdebock/ansible-role-ansible/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.ansible
```

The machine needs to be prepared in CI this is done using `molecule/resources/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.epel
    - role: robertdebock.buildtools
    - role: robertdebock.python_pip
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for ansible

ansible_configuration:
  - option: roles_path
    value: roles
  - option: retry_files_enabled
    value: "no"
  - option: inventory
    value: inventory
  - option: stdout_callback
    value: yaml
  - option: callback_whitelist
    value: profile_roles
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-ansible/blob/master/requirements.txt).

## [Status of requirements](#status-of-requirements)

The following roles are used to prepare a system. You may choose to prepare your system in another way, I have tested these roles as well.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
| [robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions) | [![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-bootstrap)
| [robertdebock.buildtools](https://galaxy.ansible.com/robertdebock/buildtools) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-buildtools/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-buildtools/actions) | [![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-ansible-role-buildtools/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-buildtools)
| [robertdebock.epel](https://galaxy.ansible.com/robertdebock/epel) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-epel/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-epel/actions) | [![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-ansible-role-epel/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-epel)
| [robertdebock.python_pip](https://galaxy.ansible.com/robertdebock/python_pip) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-python_pip/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-python_pip/actions) | [![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-ansible-role-python_pip/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-python_pip)

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/ansible-role-ansible/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|alpine|all|
|el|8|
|debian|buster, bullseye|
|fedora|all|
|opensuse|all|
|ubuntu|focal, bionic|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.

## [Exceptions](#exceptions)

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| amazonlinux:1 | No package matching 'python3-pip' |


If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-ansible/issues)

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
