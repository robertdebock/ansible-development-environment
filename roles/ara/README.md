# [ara](#ara)

Install and configure ara on your system.

|Travis|GitHub|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-ara.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-ara)|[![github](https://github.com/robertdebock/ansible-role-ara/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-ara/actions)|[![quality](https://img.shields.io/ansible/quality/24687)](https://galaxy.ansible.com/robertdebock/ara)|[![downloads](https://img.shields.io/ansible/role/d/24687)](https://galaxy.ansible.com/robertdebock/ara)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-ara.svg)](https://github.com/robertdebock/ansible-role-ara/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.ara
```

The machine may need to be prepared using `molecule/resources/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.buildtools
    - role: robertdebock.epel
    - role: robertdebock.python_pip
```

For verification `molecule/resources/verify.yml` runs after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: no

  tasks:
    - name: check if connection still works
      ping:
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for ara

# The ansible.cfg to modify.
ara_configuration_file: /etc/ansible/ansible.cfg

# The user to run ara as. Typically root, but if you run playbooks under your username, ara saves data in your homedirectory. In that case change the ara_user to your username.
ara_user: root

# Extra options can be set using this structure.
# ara_configuration:
#   - option: port
#     value: 9191
#   - option: host
#     value: 0.0.0.0
#   - option: playbook_per_page
#     value: 10
#   - option: result_per_page
#     value: 25
```

## [Requirements](#requirements)

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.buildtools
- robertdebock.epel
- robertdebock.python_pip
- robertdebock.service

```

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/ara.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|el|8|
|debian|buster, bullseye|
|fedora|31, 32|
|ubuntu|bionic|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.

## [Exceptions](#exceptions)

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| Alpine | Could not find a version that satisfies the requirement Django>=2.1.5 |
| CentOS | No matching distribution found for Django>=2.1.5 |
| amazonlinux:1 | No package matching 'python3-pip' |
| amazonlinux | No module named pkg_resources |


## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-ara) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-ara/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
