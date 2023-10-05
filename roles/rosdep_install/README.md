ROSDEP INSTALL
=========

Initializes Rosdep and runs Rosdep command on given directory. 

![Ansible Lint](https://github.com/bounverif/ansible-collection-ros/actions/workflows/ansible-lint.yml/badge.svg)

Requirements
------------

A valid path to run `rosdep` must be provided under `ros_source_dir`. User may define a new file path for Rosdep package lists other than default value by setting `rosdep_init_path` to a new file path. Setting this value to another should be done carefully. ROS version must be given by setting `ros_distro` variable.

Role Variables
--------------

These variables must be defined according to the usage to use this role. Definitions and required information on below.

| Variable                | Required | Default      | Choices                   | Comments                                 |
|-------------------------|----------|--------------|---------------------------|------------------------------------------|
| ros_source_dir          | yes      | `no default` | `directory path`          | A directory name. Rosdep will run under this directory. |
| rosdep_init_path        | yes      | `/etc/ros/rosdep/sources.list.d/20-default.list` | `file path`          | Indicates which place to initialize rosdep repository list file. |
| ros_distro              | yes      | `no default` | `string` | Sets Rosdep to run on which ROS distribution.   |


Dependencies
------------

Ros2 and Rosdep must be installed on the system.

Example Playbook
----------------

Assume ROS packages are found in subdirectories of `/tmp/ros/ros_packages`.

```
---
- name: Rosdep Install Role
  hosts: localhost
  connection: local
  vars:
    ros_source_dir: /tmp/ros/ros_packages/
    ros_distro: humble
  roles:
    - role: bounverif.ros.repositories
```

License
-------

See [license.md](https://github.com/bounverif/ansible-collection-ros/blob/main/LICENSE)

Author Information
------------------

https://github.com/bounverif/ansible-collection-ros
