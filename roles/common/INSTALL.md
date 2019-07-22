Installation
=========

To use this Ansible role skeleton, as [described in Ansible Galaxy documentation](https://docs.ansible.com/ansible/latest/reference_appendices/galaxy.html#using-a-custom-role-skeleton):

```
export keep_trailing_newline=True
ansible-galaxy init --role-skeleton=/path/to/skeleton role_name
```

or add this to ansible.cfg:

```
[galaxy]
role_skeleton = /path/to/skeleton
role_skeleton_ignore = ^.git$,^.*/.git_keep$
```

Followed by `ansible-galaxy init role_name`.

Don't include `ansible-role` to the role name, for example use `java` instead of `ansible-role-java`.
