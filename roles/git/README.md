git
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-git"><img src="https://travis-ci.org/robertdebock/ansible-role-git.svg?branch=master" alt="Build status" align="left"/></a>

Install and configure git on your system.

Example Playbook
----------------

This example is taken from `molecule/resources/playbook.yml`:
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
    - robertdebock.git
```

The machine you are running this on, may need to be prepared.
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

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

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
git_repository_destination: /home/{{ git_username }}/Documents/github.com/{{ git_username }}


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

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap

```

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/git.png "Dependency")


Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.7|ansible 2.8|ansible devel|
|------------|-----------|-----------|-------------|
|alpine-edge*|yes|yes|yes*|
|alpine-latest|yes|yes|yes*|
|archlinux|yes|yes|yes*|
|centos-6|yes|yes|yes*|
|centos-latest|yes|yes|yes*|
|debian-stable|yes|yes|yes*|
|debian-unstable*|yes|yes|yes*|
|fedora-latest|yes|yes|yes*|
|fedora-rawhide*|yes|yes|yes*|
|opensuse-leap|yes|yes|yes*|
|ubuntu-devel*|yes|yes|yes*|
|ubuntu-latest|yes|yes|yes*|
|ubuntu-rolling|yes|yes|yes*|

A single star means the build may fail, it's marked as an experimental build.

Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-git) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-git/issues)

To test this role locally please use [Molecule](https://github.com/ansible/molecule):
```
pip install molecule
molecule test
```

To test on Amazon EC2, configure [~/.aws/credentials](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) and set a region using `export AWS_REGION=eu-central-1` before running `molecule test --scenario-name ec2`.

There are many specific scenarios available, please have a look in the `molecule/` directory.

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/)
