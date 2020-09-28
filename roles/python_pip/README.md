# [python_pip](#python_pip)

Install pythons pip on your system.

|Travis|GitHub|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-python_pip.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-python_pip)|[![github](https://github.com/robertdebock/ansible-role-python_pip/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-python_pip/actions)|[![quality](https://img.shields.io/ansible/quality/42440)](https://galaxy.ansible.com/robertdebock/python_pip)|[![downloads](https://img.shields.io/ansible/role/d/42440)](https://galaxy.ansible.com/robertdebock/python_pip)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-python_pip.svg)](https://github.com/robertdebock/ansible-role-python_pip/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.python_pip
```

The machine may need to be prepared using `molecule/resources/prepare.yml`:
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
```

For verification `molecule/resources/verify.yml` runs after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: no

  tasks:
    - name: install pip module
      pip:
        name: docker
        state: present

    - name: check if bootstrap still works.
      include_role:
        name: robertdebock.bootstrap

    - name: remove pip module
      pip:
        name: docker
        state: absent

    - name: check if requested modules can be installed
      include_role:
        name: robertdebock.python_pip
      vars:
        python_pip_modules:
          - name: docker
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for python_pip

# By default no modules should be installed.
python_pip_modules: []

# Connect to a (pypi) proxy by setting this variable.
# python_pip_proxy: "https://user:password@proxy:8443/artifactory/pypi/pypi-virtual/simple"

# Don't forget to trust foreign pip repositories if you use them.
# python_pip_trusted_host: my-pip-repository.example.com
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

```

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/python_pip.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|alpine|all|
|el|7, 8|
|debian|buster, bullseye|
|fedora|31, 32|
|opensuse|all|
|ubuntu|focal, bionic, xenial|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.

## [Exceptions](#exceptions)

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| amazonline:1 | ImportError: No module named pkg_resources |
| amazonline | ImportError: No module named pkg_resources |


## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-python_pip) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-python_pip/issues)

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

## [Contributors](#contributors)

I'd like to thank everybody that made contributions to this repository. It motivates me, improves the code and is just fun to collaborate.

- [rohankrishnadev](https://github.com/rohankrishnadev)

## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
