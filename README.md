# Ansible development environment

Setup a machine to write Ansible roles. Includes:
- [ansible](https://github.com/ansible)
- [ansible-lint](https://github.com/ansible/ansible-lint)
- [molecule](https://molecule.readthedocs.io/en/latest/)
- [travis (cli)](https://github.com/travis-ci/travis.rb)
- [ara](https://github.com/openstack/ara)

## Download

In some directory, maybe `Documents` run:

```sh
git clone https://github.com/robertdebock/ansible-development-environment
cd ansible-development-environment
```

## Setup

Download all required roles:

```sh
ansible-galaxy install --role-file roles/requirements.yml
```

Now change a few files:

- `files/gitconfig` should contain your details.
- `files/id_rsa` should contain an ssh-key used to commit to GitHub.
- `inventory/hosts` should contain your machine.
- `inventory/group_vars/all.yml` should contain your details.

## Install

Simply run `./playbook.yml`. Preparing your system will take about 15 minutes or so.

## Code

You are now ready to code! Have fun using these commands:

```sh
# See if your code meets all rules.
ansible-lint .
# Test all scenarios.
molecule test
# Test a specific scenario.
molecule test --scenario-name fedora-latest
```

You can see the playbook runs on https://localhost:9191/
