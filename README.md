# Postgresql Server

Master: [![Build Status](https://travis-ci.org/sansible/postgresql.svg?branch=master)](https://travis-ci.org/sansible/postgresql)  
Develop: [![Build Status](https://travis-ci.org/sansible/postgresql.svg?branch=develop)](https://travis-ci.org/sansible/postgresql)

* [Installation and Dependencies](#installation-and-dependencies)
* [Tags](#tags)
* [Examples](#examples)

This roles installs Postgresql server.


## Installation and Dependencies

To install this role run `ansible-galaxy install sansible.postgresql` or add
this to your `roles.yml`.

```YAML
- src: sansible.postgresql
  version: v2.0
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

To simply install Postgresql and allow all connections.

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
      sansible_postgresql_listen_addresses: "*"
      sansible_postgresql_hba_conf:
        - type: local
          user: postgres
          auth_method: trust
        - type: host
          address: "0.0.0.0/0"
```
