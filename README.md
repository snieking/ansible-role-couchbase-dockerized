Ansible Role: Couchbase Dockerized
=========
[![Build Status](https://travis-ci.org/snieking/ansible-role-couchbase-dockerized.svg?branch=master)](https://travis-ci.org/snieking/ansible-role-couchbase-dockerized)
[![Ansible Role](https://img.shields.io/ansible/role/d/3078.svg)](https://galaxy.ansible.com/snieking/couchbase_dockerized)

Runs a dockerized couchbase with necessary OS configuration for production environments.

There are many good reasons to run Couchbase in a dockerized environment. The main reason is that it is much easier to upgrade/downgrade versions. Just spin up a new container with a different version.

Requirements
------------
The role requires **python-pip** to be installed and available on the hosts.

Docker is also required to be installed on the hosts. A good tip is to add [geerlingguy.docker](https://galaxy.ansible.com/geerlingguy/docker) role from Ansible Galaxy to your playbook before this role is executed.

**Also make sure that the user is in the docker group.**

Role Variables
--------------

The role comes with a couple of default values.

**couchbase_version: enterprise-5.5.2** \
Look at [couchbase/server]() for available versons.

**couchbase_docker_volume_dir: /opt/couchbase/var** \
Volume for persisting the Couchbase data.

Dependencies
------------

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```yaml
- hosts: servers
  roles:
    - role: geerlingguy.docker
      become: yes
  post_tasks:
    - name: add to docker group
      user:
        name: "{{ ansible_user }}"
        groups: docker
      become: yes
    - name: install pip
      easy_install:
        name: pip
        state: latest
      become: yes

- hosts: servers
  roles:
    - role: snieking.couchbase_dockerized
      couchbase_version: enterprise-5.1.1
      couchbase_docker_volume_dir: /home/snieking/couchbase/var
```

License
-------

BSD, MIT

Author Information
------------------

Viktor Plane [https://thecuriousdev.org](https://thecuriousdev.org)