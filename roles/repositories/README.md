REPOSITORIES
=========

Reads repos file contents similar to existing VCS tool, downloads the repositories in indicated repos file. Downloads repositories from dictionary lists.

![Ansible Lint](https://github.com/bounverif/ansible-collection-ros/actions/workflows/ansible-lint.yml/badge.svg)

Requirements
------------

A valid path to a directory in which includes files written in `repos` format no matter what is the file name, or a valid list constructed by dictionaries which have `ansible.builtin.git` module's parameters. 

For file reading define `repositories_files` which is a string of a relative or absolute directory path. Define `repositories_files` that is a list of strings constructed by only file names. The repository will read `<collection_name>/files/` directory in the collection. Do not define any `repositories` named list or variable. Until then, it will work same as the VCS tool. Also define `collection_name` as the real collection name.

For variable reading define a `repositories` list variable which consists of dictionaries that have parameters of `ansible.builtin.git` module. Do not define the variable `repositories_files`.

Role Variables
--------------

These variables must be defined according to the usage to use this role. Definitions and required information on below.

| Variable                | Required | Default      | Choices                   | Comments                                 |
|-------------------------|----------|--------------|---------------------------|------------------------------------------|
| ros_source_dir          | yes      | `no default` | `directory path`          | A directory name. Required when read_repositories_from_file is set `true`. |
| repositories            | yes      | `no default` | `list of dictionaries`    | List of dictionaries with fields named as git builtin. Do not define if `repositories_files` set. |
| repositories_files | yes      | `no default` | `list of file names`      | Names of files will be read. If defined, then the role will read files instead of `repositories` list.|
| collection_name         | yes      | `no default` | `name of collection`      | Name of your own collection. |


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
    ros_source_dir: "/tmp/ros/examples/sample_repos_file/" 
    repositories_files:
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
      - { url: https://github.com/some/git/repository1.git, dest: "to/some/download/path/", version: main }
      - { url: https://github.com/some/git/repository2.git, dest: "to/some/download/path/", version: main }
  roles:
    - role: bounverif.ros.repositories
```

License
-------

See [license.md](https://github.com/bounverif/ansible-collection-ros/blob/main/LICENSE)

Author Information
------------------

https://github.com/bounverif/ansible-collection-ros
