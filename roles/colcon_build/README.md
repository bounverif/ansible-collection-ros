COLCON BUILD
=========

Runs the `colcon build` command.

![Ansible Lint](https://github.com/bounverif/ansible-collection-ros/actions/workflows/ansible-lint.yml/badge.svg)

Requirements
------------

A valid path to a ROS2 workspace must be given.

Role Variables
--------------

Two global variables must be defined to use this role. Definitions and required information on below.

| Variable                | Required | Default      | Choices                   | Comments                                 |
|-------------------------|----------|--------------|---------------------------|------------------------------------------|
| ros_workspace           | yes      | `no default` | `directory path`          | A directory name. ROS2 workspace directory must be provided. |
| colcon_build_build_base_dir | yes  | `./build`    | `directory path`          | Colcon build directory argument. Colcon builds the libraries under specified directory. |
| colcon_build_install_base_dir | yes| `./install`  | `directory path`          | Colcon install directory argument. Colcon installs the specified programs under specified directory.|
| colcon_build_merge_install | no    | `false`      | `bool value`              | Merge install option usage. For details see Colcon documentation. |
| colcon_build_symlink_install | no  | `true`       | `bool value`              | Symlik install option usage. For details see Colcon documentation. |
| colcon_build_test_result_base | no | `false`      | `bool_value`              | Test result enable option. |
| colcon_build_test_result_base_dir | no| `colcon_build_build_base_dir`| `directory path` | Working directory for test result option. For details see Colcon documentation. |
| colcon_build_continue_on_error | no| `false`      | `bool value`              | Continue execution even if an error occurs. For details see Colcon documentation. |
| colcon_build_use_cmake_args  | no  | `true`       | `bool value`              | Indicates whether user cmake args flag or not. |
| colcon_build_cmake_args       | no | `"-DCMAKE_BUILD_TYPE=Release"`| `directory path` | CMake arguments that will be called while CMake running. |
| colcon_build_packages_up_to | no   | `no default` | `list of package names (string)`  | Packages are installed up to given package name. For more details see Colcon documentation. |


Dependencies
------------

This role does not require any other roles. All the required variables should be defined by user in a proper way, for example in an Ansible playbook.

Example Playbook
----------------

An example playbook is provided below:

```
---
- name: Colcon Build Role
  hosts: localhost
  connection: local
  
  vars:
    ros_workspace: "/tmp/workspace/"
    colcon_build_build_base_dir: "/tmp/workspace/build"
    colcon_build_install_base_dir: "/tmp/workspace/install"
    colcon_build_symlink_install: true
    colcon_build_use_cmake_args: true
    colcon_build_cmake_args: "-DCMAKE_BUILD_TYPE=Release"
    colcon_build_packages_up_to: 
      - package1
      - package2
    
  roles:
    - role: bounverif.ros.colcon_build
```

License
-------

See [license.md](https://github.com/bounverif/ansible-collection-ros/blob/main/LICENSE)

Author Information
------------------

https://github.com/bounverif/ansible-collection-ros
