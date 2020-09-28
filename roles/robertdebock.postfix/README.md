# [postfix](#postfix)

Install and configure postfix on your system.

|Travis|GitHub|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-postfix.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-postfix)|[![github](https://github.com/robertdebock/ansible-role-postfix/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-postfix/actions)|[![quality](https://img.shields.io/ansible/quality/22976)](https://galaxy.ansible.com/robertdebock/postfix)|[![downloads](https://img.shields.io/ansible/role/d/22976)](https://galaxy.ansible.com/robertdebock/postfix)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-postfix.svg)](https://github.com/robertdebock/ansible-role-postfix/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.postfix
      postfix_myhostname: "smtp.example.com"
      postfix_mydomain: "example.com"
      postfix_myorigin: "example.com"
      postfix_aliases:
        - name: root
          destination: test@example.com
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
    - role: robertdebock.core_dependencies
```

For verification `molecule/resources/verify.yml` runs after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: no

  tasks:
    - name: check if port 25 is open
      wait_for:
        port: 25

    - name: check if a mail can be sent
      mail:
        from: "Robert de Bock <robert@example.com>"
        to: "Robert de Bock <root@example.com>"
        subject: Testing robertdebock.postfix.
        body: Testing the ansible role postfix.
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for postfix

# These settings are required in postfix.
postfix_myhostname: "{{ ansible_fqdn }}"
postfix_mydomain: "{{ ansible_domain | default('localdomain', true) }}"
postfix_myorigin: "{{ ansible_domain | default('localdomain', true) }}"

# To "listen" on public interfaces, set inet_interfaces to something like
# "all" or the name of the interface, such as "eth0".
postfix_inet_interfaces: "loopback-only"

# Enable IPv4, and IPv6 if supported - if IPV4 only set to ipv4
postfix_inet_protocols: all

# The distination tells Postfix what mails to accept mail for.
postfix_mydestination: $mydomain, $myhostname, localhost.$mydomain, localhost

# To accept email from other machines, set the mynetworks to something like
# "192.168.0.0/24".
postfix_mynetworks: "127.0.0.0/8"

# These settings change the role of the postfix server to a relay host.
# postfix_relay_domains: "$mydestination"

# If you want to forward emails to another central relay server, set relayhost.
# use brackets to sent to the A-record of the relayhost.
# postfix_relayhost: [relay.example.com]

# Set the restrictions for receiving mails.
postfix_smtpd_recipient_restrictions:
  - permit_mynetworks
  - permit_sasl_authenticated
  - reject_unauth_destination
  - reject_invalid_hostname
  - reject_non_fqdn_hostname
  - reject_non_fqdn_sender
  - reject_non_fqdn_recipient
  - reject_unknown_sender_domain
  - reject_unknown_recipient_domain
  - reject_rbl_client sbl.spamhaus.org
  - reject_rbl_client cbl.abuseat.org
  - reject_rbl_client dul.dnsbl.sorbs.net
  - permit

postfix_smtpd_sender_restrictions:
  - reject_unknown_sender_domain

# To enable spamassassin, ensure spamassassin is installed,
# (hint: role: robertdebock.spamassassin) and set these two variables:
# postfix_spamassassin: enabled
# postfix_spamassassin_user: spamd

# To enable clamav, ensure clamav is installed,
# (hint: role: robertdebock.clamav) and set this variable:
# postfix_clamav: enabled

# You can configure aliases here. Typically redirecting `root` is a good plan.
# postfix_aliases:
#   - name: root
#     destination: robert@meinit.nl

# You can configure sender access controls here.
# postfix_sender_access:
#   - domain: gooddomain.com
#     action: OK
#   - domain: baddomain.com
#     action: REJECT

# You can configure recipient access controls here.
# postfix_recipient_access:
#   - domain: gooddomain.com
#     action: OK
#   - domain: baddomain.com
#     action: REJECT
```

## [Requirements](#requirements)

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.core_dependencies

```

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/postfix.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|amazon|2018.03|
|el|7, 8|
|debian|buster, bullseye|
|fedora|31, 32|
|ubuntu|focal, bionic, xenial|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.

## [Exceptions](#exceptions)

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| opensuse | Not idempotent on configure postfix (main.cf) and configure postfix |
| alpine | 451, 4.3.0 <root@example.com>: Temporary lookup failure |


## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-postfix) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-postfix/issues)

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
