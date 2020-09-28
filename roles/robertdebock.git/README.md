# [git](#git)

Install and configure git on your system.

|Travis|GitHub|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-git.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-git)|[![github](https://github.com/robertdebock/ansible-role-git/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-git/actions)|[![quality](https://img.shields.io/ansible/quality/34950)](https://galaxy.ansible.com/robertdebock/git)|[![downloads](https://img.shields.io/ansible/role/d/34950)](https://galaxy.ansible.com/robertdebock/git)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-git.svg)](https://github.com/robertdebock/ansible-role-git/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  vars:
    git_username: root
    git_groupname: root
    git_repository_destination: /root
    git_repositories:
      - repo: https://github.com/robertdebock/robertdebock.bootstrap
        dest: bootstrap
      - repo: https://github.com/robertdebock/robertdebock.bootstrap
        dest: bootstrap-force
        force: yes
      - repo: https://github.com/robertdebock/robertdebock.bootstrap
        dest: bootstrap-version
        version: 2.11.1

  roles:
    - role: robertdebock.git
```

The machine may need to be prepared using `molecule/resources/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes
  serial: 30%

  roles:
    - role: robertdebock.bootstrap
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
# defaults file for git

# The system username in /home where to place the gitconfig file.
# git_username: johndoe

# The group to own directories.
# git_groupname: "{{ git_username }}"

# Settings for git configuration.
# git_user_email: johndoe@example.com
# git_user_name: John Doe

# Where to place the copies of the repositories.
git_repository_destination: /home/{{ git_username | default('unset') }}/Documents/github.com/{{ git_username | default('unset') }}

# Should git force (overwrite locally changed) clone? (Can also be controlled
# per repository, see below.
git_force: no

# The repositories to check out, bootstrap is pinned to a version, java will get HEAD/latest.
# git_repositories:
#   - repo: https://github.com/robertdebock/ansible-role-bootstrap.git
#     dest: bootstrap
#     version: 2.2.4
#   - repo: ssh://git@github.com/robertdebock/ansible-role-java.git
#     dest: java
#   - repo: ssh://git@github.com/robertdebock/ansible-role-tomcat.git
#     dest: tomcat
#     force: yes
```

## [Requirements](#requirements)

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap

```

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/git.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|alpine|all|
|amazon|2018.03|
|el|7, 8|
|debian|buster, bullseye|
|fedora|31, 32|
|opensuse|all|
|ubuntu|focal, bionic, xenial|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.



## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-git) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-git/issues)

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

- [langouste](https://github.com/langouste)

## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
