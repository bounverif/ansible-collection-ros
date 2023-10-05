ROS2 INSTALL
=========

Installs ROS2 and sets up Bash environment variables.

![Ansible Lint](https://github.com/bounverif/ansible-collection-ros/actions/workflows/ansible-lint.yml/badge.svg)

Requirements
------------

Proper Ubuntu distribution and version must be provided in order to complete installation.

Dependencies
------------

This role does not require any other roles or defining variables. Just run.

Example Playbook
----------------

```
---
- name: Ros2 Install Role
  hosts: localhost
  connection: local
  roles:
    - role: bounverif.ros.ros2_install
```

License
-------

See [license.md](https://github.com/bounverif/ansible-collection-ros/blob/main/LICENSE)

Author Information
------------------

https://github.com/bounverif/ansible-collection-ros
