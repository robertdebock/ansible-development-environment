# [service](#service)

Add custom services to your Linux system.

|Travis|GitHub|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-service.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-service)|[![github](https://github.com/robertdebock/ansible-role-service/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-service/actions)|[![quality](https://img.shields.io/ansible/quality/38040)](https://galaxy.ansible.com/robertdebock/service)|[![downloads](https://img.shields.io/ansible/role/d/38040)](https://galaxy.ansible.com/robertdebock/service)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-service.svg)](https://github.com/robertdebock/ansible-role-service/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  vars:
    _service_test_command:
      default: /usr/bin/sleep
      Alpine: /bin/sleep

    service_test_command: "{{ _service_test_command[ansible_os_family] | default(_service_test_command['default']) }}"

    service_list:
      - name: simple-service
        description: Simple Service
        start_command: "{{ service_test_command }} 3600"
      - name: forking-service
        description: Forking Service
        type: forking
        start_command: "{{ service_test_command }} 7200 &"
      - name: specific-stop-service
        description: Specific Stop Service
        start_command: "{{ service_test_command }} 1440"
        stop_command: killall -f "sleep 1440"
      - name: specific-user-group-service
        description: Specific User Group Service
        start_command: "{{ service_test_command }} 28800"
        user_name: root
        group_name: root
      - name: specific-workingdirectory-service
        description: Specific WorkingDirectory Service
        start_command: "{{ service_test_command }} 57600"
        working_directory: /tmp
      - name: specific-pattern-service
        description: Specific Status Pattern Service
        start_command: "{{ service_test_command }} 115200"
        status_pattern: 115200
      - name: variable-service
        description: Service with environment variables
        start_command: "{{ service_test_command }} ${time}"
        environment_variables:
          time: 230400

  roles:
    - role: robertdebock.service
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

For verification `molecule/resources/verify.yml` run after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: yes

  vars:
    service_list:
      - name: simple-service

  tasks:
    - name: start simple-service
      service:
        name: simple-service
        state: started

    - name: stop simple-service
      service:
        name: simple-service
        state: stopped

    - name: restart simple-service
      service:
        name: simple-service
        state: restarted
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for service

# service_list can contain a list of services to add to the system.
# The mandatory items for each item are:
# - name: The (short) name of the service, i.e. "tomcat".
# - description: A bit longer name, i.e. "Tomcat application server".
# - start_command: The command to start the daemon,
#   i.e. "/usr/local/bin/java -jar some.jar"
# The optional items are:
# - stop_command: By default the program that is started is found and stopped.
#   in case a running program is renamed or expanded (including a path) during
#   startup, you can specify a custom stop command here, i.e. "pkill foo"
# - status_pattern: What program (or pattern) to look for when finding the
#   status of a program, i.e. "artifactory".
# - type: How the program starts; "simple" or "forking". Simple means the
#   program runs on the foreground, i.e. "nc -l 1234". Forking means the
#   program itself forks, i.e. "nc -l 12345 &"
# - working_directory: The directory to cd into before starting the service.
# - environment_variables: A list for variables to set. for example:
#   environment_variables:
#     variable1: value1
#     variable2: value2
# - after: Start after the mentioned service.
# - restart_mode: The mode to use, for example "always".
# - restart_seconds: The time to allow restart to finish.
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
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/service.png "Dependency")

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

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-service) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-service/issues)

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

- [githengi](https://github.com/githengi)

## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
