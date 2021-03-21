# [docker](#docker)

Install and configure Docker (non-CE) on your system.

|GitHub|GitLab|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![github](https://github.com/robertdebock/ansible-role-docker/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-docker/actions)|[![gitlab](https://gitlab.com/robertdebock/ansible-role-docker/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-docker)|[![quality](https://img.shields.io/ansible/quality/21647)](https://galaxy.ansible.com/robertdebock/docker)|[![downloads](https://img.shields.io/ansible/role/d/21647)](https://galaxy.ansible.com/robertdebock/docker)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-docker.svg)](https://github.com/robertdebock/ansible-role-docker/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.docker
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
    - role: robertdebock.core_dependencies
    - role: robertdebock.buildtools
    - role: robertdebock.epel
    - role: robertdebock.python_pip
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.


## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-docker/blob/master/requirements.txt).

## [Status of requirements](#status-of-requirements)

The following roles are used to prepare a system. You may choose to prepare your system in another way, I have tested these roles as well.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
| [robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions) | [![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-bootstrap)
| [robertdebock.buildtools](https://galaxy.ansible.com/robertdebock/buildtools) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-buildtools/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-buildtools/actions) | [![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-ansible-role-buildtools/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-buildtools)
| [robertdebock.core_dependencies](https://galaxy.ansible.com/robertdebock/core_dependencies) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-core_dependencies/actions) | [![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-ansible-role-core_dependencies/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-core_dependencies)
| [robertdebock.epel](https://galaxy.ansible.com/robertdebock/epel) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-epel/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-epel/actions) | [![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-ansible-role-epel/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-epel)
| [robertdebock.python_pip](https://galaxy.ansible.com/robertdebock/python_pip) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-python_pip/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-python_pip/actions) | [![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-ansible-role-python_pip/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-python_pip)

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/ansible-role-docker/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|alpine|all|
|el|8|
|debian|buster, bullseye|
|fedora|all|
|ubuntu|focal, bionic|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.

## [Exceptions](#exceptions)

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| Ubuntu | Unable to find any of pip2, pip to use. |
| amazonlinux | Required dependency (python_pip) does not work on amazonlinux. |


If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-docker/issues)

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
