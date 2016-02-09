# Postgresql Server

Master: [![Build Status](https://travis-ci.org/sansible/postgresql.svg?branch=master)](https://travis-ci.org/sansible/postgresql)  
Develop: [![Build Status](https://travis-ci.org/sansible/postgresql.svg?branch=develop)](https://travis-ci.org/sansible/postgresql)

* [ansible.cfg](#ansible-cfg)
* [Installation and Dependencies](#installation-and-dependencies)
* [Tags](#tags)
* [Examples](#examples)

This roles installs Postgresql server.




## ansible.cfg

This role is designed to work with merge "hash_behaviour". Make sure your
ansible.cfg contains these settings

```INI
[defaults]
hash_behaviour = merge
```




## Installation and Dependencies

To install this role run `ansible-galaxy install sansible.postgresql` or add
this to your `roles.yml`.

```YAML
- src: sansible.postgresql
  version: v1.0
```

and run `ansible-galaxy install -p ./roles -r roles.yml`




## Tags

This role uses two tags: **build** and **configure**

* `build` - Installs Postgresql server.
* `configure` - Configures and ensures that the service is running.




## Examples

To simply install Postgresql server:

```YAML
- name: Install Postgresql
  hosts: sandbox

  pre_tasks:
    - name: Update apt
      become: yes
      apt:
        cache_valid_time: 1800
        update_cache: yes
      tags:
        - build

  roles:
    - role: sansible.postgresql
```
