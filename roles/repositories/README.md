REPOSITORIES
=========

Reads repos file contents similar to existing VCS tool, downloads the repositories in indicated repos file.

![Ansible Lint](https://github.com/bounverif/ansible-collection-ros/actions/workflows/ansible-lint.yml/badge.svg)

Requirements
------------

At least one repos file is required. The directory including those repos files must be given by assigning `ros_repos_directory` variable to a path pointing a directory.


Role Variables
--------------

Two global variables must be defined to use this role. Definitions and required information on below.

| Variable                | Required | Default      | Choices                   | Comments                                 |
|-------------------------|----------|--------------|---------------------------|------------------------------------------|
| ros_repos_directory     | yes      | `no default` | `directory path`          | Must end with / character.               |
| ros_source_dir          | yes      | `no default` | `directory path`          | Indicates where to download repositories.|

Dependencies
------------

This role does not require any other roles. All the required variables should be defined by user, for example in an Ansible playbook.

Example Playbook
----------------

An example playbook with only necessary values to run this role on localhost. For this case the directory to download repositories is `"/tmp/ros/src/"` and repos files are in `"/tmp/ros/examples/sample_repos_file/"`

```
---
- name: Build Autoware and dependencies
  hosts: localhost
  #no_log: true
  connection: local
  vars:
    ros_source_dir: "/tmp/ros/src"
    ros_repos_directory: "/tmp/ros/examples/sample_repos_file/"
  roles:
    - role: bounverif.ros.repositories
```

License
-------

See [license.md](https://github.com/bounverif/ansible-collection-ros/blob/main/LICENSE)

Author Information
------------------

https://github.com/bounverif/ansible-collection-ros
