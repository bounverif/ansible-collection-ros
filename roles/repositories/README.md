REPOSITORIES
=========

Reads repos file contents similar to existing VCS tool, downloads the repositories in indicated repos file. Downloads repositories from dictionary lists.

![Ansible Lint](https://github.com/bounverif/ansible-collection-ros/actions/workflows/ansible-lint.yml/badge.svg)

Requirements
------------

A valid path to a directory in which includes files written in `repos` format, or a valid list constructed by dictionaries which have `ansible.builtin.git` module's parameters. 

For file reading define `repos_directory` which is a string of a relative or absolute directory path, that directory can also be defined by defining `ROS_WORKSPACE` environment variable. Define `repositories_file_names` that is a list of strings constructed by file names. Do not define any `repositories` named list or variable. Define `download_dir` as a directory, if the repository is not defined a specific `dest` value, then the files will be downloaded onto `download_dir`.

For variable reading define a `repositories` list variable which consists of dictionaries that have parameters of `ansible.builtin.git` module. Do not define the variable `repositories_file_names`.

Role Variables
--------------

These variables must be defined according to the usage to use this role. Definitions and required information on below.

| Variable                | Required | Default      | Choices                   | Comments                                 |
|-------------------------|----------|--------------|---------------------------|------------------------------------------|
| repos_directory         | yes      | `no default` | `directory path`          | A directory name. Required when read_repositories_from_file is set `true`. |
| download_dir            | yes      | `no default` | `directory path`          | Indicates where to download repositories if `dest` parameter on git parameter is not set. |
| repositories            | yes      | `no default` | `list of dictionaries`    | List of dictionaries with fields named as git builtin. Do not define if `read_repositories_from_file` set. |
| repositories_file_names | yes      | `no default` | `list of file names`      | Names of files will be read. If defined, then the role will read files instead of `repositories` list.|


Dependencies
------------

This role does not require any other roles. All the required variables should be defined by user in a proper file, for example in an Ansible playbook.

Example Playbook
----------------

An example playbook using file read feature, runs this role on localhost. For this case the directory to download repositories is `"/tmp/ros/src/"` and repos files are in `"/tmp/ros/examples/sample_repos_file/"`. In this example file names are `file1.repos` and `file2.yaml`.

```
---
- name: Repositories Role - File Read
  hosts: localhost
  connection: local
  vars:
    repos_directory: "/tmp/ros/examples/sample_repos_file/" 
    download_dir: "/tmp/ros/src"
    repositories_file_names:
      - file1.repos
      - file2.yaml
    
  roles:
    - role: bounverif.ros.repositories
```

```
- name: Repositories Role - Variable Read
  hosts: localhost
  connection: local
  vars:
    repositories:
      - { url: https://github.com/some/git/repository1.git, dest: "/to/some/download/path/", version: main }
      - { url: https://github.com/some/git/repository2.git, dest: "/to/some/download/path", version: main }
  roles:
    - role: bounverif.ros.repositories
```

License
-------

See [license.md](https://github.com/bounverif/ansible-collection-ros/blob/main/LICENSE)

Author Information
------------------

https://github.com/bounverif/ansible-collection-ros
