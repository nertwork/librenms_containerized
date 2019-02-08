<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [ansible-librenms-containerized](#ansible-librenms-containerized)
  - [Requirements](#requirements)
  - [Role Variables](#role-variables)
  - [Dependencies](#dependencies)
    - [Recommended to use the following roles:](#recommended-to-use-the-following-roles)
  - [First run gotchas](#first-run-gotchas)
    - [Before Running this role](#before-running-this-role)
  - [Example Playbook](#example-playbook)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
# ansible-librenms-containerized

An all-in one [Ansible](https://www.ansible.com) [MariaDB](https://www.ansible.com) and [LibreNMS](https://www.librenms.org/) Deployment
> NOTE: This is a docker container deployment

## Requirements
- Docker
- Python
- Python-Pip
- Ansible 2.2+

## Role Variables
Required variables: 
- `app_key: "base64:Q0+ZV56/5Uwz79vsvS4ZfwQFOty3e9DJEouEy+IXvz8="`

Replace "base64:Q0+ZV56/5Uwz79vsvS4ZfwQFOty3e9DJEouEy+IXvz8=" with your own app key

[defaults/main.yml](defaults/main.yml)

Other variables can be set in defaults/all.yml file:

## Dependencies

### Recommended to use the following roles:
- name: geerlingguy.docker
- name: geerlingguy.pip

## First run gotchas

### Before Running this role

You must obtain an app key for librenms docker, this can be done by running the following:

`docker run --rm jarischaefer/docker-librenms generate_key`

## Example Playbook
```
- name: Setup LibreNMS Server
  hosts: librenms
  become: true
  tags: librenms

  tasks:
    - name: include docker role
      include_role:
        name: geerlingguy.docker

    - name: include pip role
      include_role:
        name: geerlingguy.pip
      vars:
        pip_install_packages:
          - name: docker

    - name: include librenms role
      include_role:
        name: nertwork.librenms_containerized
```
