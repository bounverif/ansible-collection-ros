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
| rosdep_init_path        | no       | `/etc/ros/rosdep/sources.list.d/20-default.list` | `file path`          | Indicates which place to initialize rosdep repository list file. |
| ros_distro              | yes      | `no default` | `string`                  | Sets Rosdep to run on which ROS distribution.   |
| rosdep_install_default_yes | no    | `true`       | `bool`                    | Say yes automatically to all install candidates flag, --default-yes. For details see Rosdep documentation. |
| rosdep_install_continue_installing | no | `true`  | `bool`                    | Continue installing even if an error occurs flag, -r. For details see Rosdep documentation. |
| rosdep_install_select_all_packages | no | `false` | `bool`                    | Flag -a, select all packages. For details see Rosdep documentation. |
| rosdep_install_quiet    | no       | `false`      | `bool`                    | Flag -q, quiet mode. For details see Rosdep documentation. |
| rosdep_install_ignore_recursive | no | `false`    | `bool`                    | Flag -n, ignore recursive dependencies. For details see Rosdep documentation. |
| rosdep_install_ignore_src | no     | `true`       | `bool`                    | Flag --ignore-src, ignores source file dependencies. For details see Rosdep documentation. |
| rosdep_install_include_eol_distros | no | `false` | `bool`                    | Flag --include-eol-distros, includes end-of-life ROS distribution for dependency checking. For details see Rosdep documentation. |
| rosdep_install_reinstall | no      | `false`      | `bool`                    | Flag --reinstall, reinstalls packages even if they are already be installed. For details see Rosdep documentation. |
| rosdep_install_dependency_types | no | `list`     | `list`                    | Flag --dependency-types (and -t), applies the options given as string list. For every item in this list it adds another flag and value pair to overall command. If not defined, then the Rosdep installs all except `doc`. For details see Rosdep documentation. |

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
    rosdep_install_default_yes: true
    rosdep_install_quiet: true
    rosdep_install_ignore_src: true
    rosdep_install_include_eol_distros: false
    rosdep_install_reinstall: false
    rosdep_install_dependency_types:
      - buildtool
      - exec
      - doc
      - buildtool_export
      - build_export
      - build
      - test
    
  roles:
    - role: bounverif.ros.repositories
```

License
-------

See [license.md](https://github.com/bounverif/ansible-collection-ros/blob/main/LICENSE)

Author Information
------------------

https://github.com/bounverif/ansible-collection-ros
