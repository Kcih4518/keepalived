# Ansible Role: Keepalived

[![CI](https://github.com/geerlingguy/ansible-role-haproxy/workflows/CI/badge.svg?event=push)](https://github.com/Kcih4518/keepalived/actions?query=workflow%3ACI)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-haproxy-blue.svg)](https://galaxy.ansible.com/Oefenweb/haproxy)

Installs Keepalived for kubernetes on Ubuntu Linux servers.

**Note**: This role _officially_ supports Keepalived versions 2.0.20.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    k8s_control_plane_virtual_ip: 127.0.0.1
    keepalived_unicast_peers: "{% for host in groups['masters'] %}'{{ hostvars[host]['ansible_host'] }}'{% if not loop.last %},{% endif %}{% endfor %}"
    keepalived_password: 'd0cker'
    keepalived_priority: "{% if inventory_hostname == groups['masters'][0] %}150{% elif inventory_hostname == groups['masters'][1] %}120{% else %}80{% endif %}"
    keepalived_router_id: 51

## Example Playbook

    - hosts: kubernetes-master
      become: true
      roles:
        - { role: kcih4518.keepalived }

## Author Information

This role was created in 2022 by [Avery Yang](https://www.linkedin.com/in/avery-yang-85b554144/).
