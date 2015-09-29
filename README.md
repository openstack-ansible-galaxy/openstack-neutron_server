Neutron server OpenStack Ansible Role
=========

**Status**
* [![Build Status](https://travis-ci.org/openstack-ansible-galaxy/openstack-neutron_server.svg?branch=master)](https://travis-ci.org/openstack-ansible-galaxy/openstack-neutron_server) on master branch
* [![Build Status](https://travis-ci.org/openstack-ansible-galaxy/openstack-neutron_server.svg?branch=development)](https://travis-ci.org/openstack-ansible-galaxy/openstack-neutron_server) on development branch
* [![Ansible Galaxy](http://img.shields.io/badge/dguerri-openstack--neutron_server-blue.svg)](https://galaxy.ansible.com/list#/roles/1780) on Ansible Galaxy

OpenStack Neutron server installation

_Tested on Ubuntu Precise (12.04) and Trusty (14.04)_

Requirements
------------

A RabbitMQ server. See below.

A Keystone server. See below.

A Nova API server. See below.

For RHEL/CentOS, RHOSP or RDO repositories are needed.

Role Variables
--------------

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `neutron_dbpass` | `neutron_dbpass_default` | neutron user db password ||
| `neutron_server_hostname` | `localhost` | Hostname/IP address where this role runs, it will be used to set keystone endpoints  ||
| `neutron_port` | `9696` | Desired neutron-server port ||
| `neutron_protocol` | `http` | Desired neutron protocol (http/https) | WiP, do not use |
| `neutron_user` | `neutron` | Neutron user as defined on Keystone ||
| `neutron_pass` | `neutron_pass_default` | Neutron password as defined on Keystone ||
| `nova_api_hostname` | `localhost` | Hostname/IP address where the Nova API service runs ||
| `nova_user` | `nova` | Nova API service username ||
| `nova_pass` | `nova_pass_default` | Nova API service password ||
| `nova_port` | `8774` | Nova API service port ||
| `nova_protocol` | `http` | Desired glance protocol (http/https) ||
| `nova_admin_tenant_id` | false | Desired service tenant id | if false, tenant id of `service` tentant will be used. Note that to retrieve that `neutron_user` must be admin in `service` tenant |
| `keystone_admin_token` | `admin_token_default` | Keystone admin service token ||
| `keystone_admin_port` | `35357` | Keystone admin service port ||
| `keystone_hostname` | `localhost` | Hostname/IP address where the keystone service runs ||
| `keystone_port` | `5000` | Keystone service port ||
| `keystone_protocol` | `http` | Desired keystone protocol (http/https) ||
| `neutron_rabbit_hostname` | `localhost` | Hostname/IP address where the RabbitMQ service runs ||
| `neutron_rabbit_username` | `rabbit_username_default` | RabbitMQ username for neutron ||
| `neutron_rabbit_pass` | `rabbit_pass_default` | RabbitMQ password for neutron ||
| `neutron_rabbit_virtual_host` | `/` | RabbitMQ virtual host ||
| `neutron_rabbit_retry_interval` | `1` | Frequency to retry connecting to RabbitMQ ||
| `neutron_rabbit_hosts` | `$rabbit_host:$rabbit_port` | RabbitMQ HA Cluster host:port pairs ||
| `neutron_rabbit_ha_queues` | `False` | Use HA queues in RabbitMQ (x-ha-policy:all) ||


Dependencies
------------

None

Example Playbook
----------------

    - hosts: neutron_server001
      roles:
        - role: openstack-neutron_server
           mysql_rootpass: "{{ MYSQL_ROOT }}"
           rabbit_username: "openstack-neutron"
           rabbit_pass: "{{ RABBIT_NEUTRON_PASS }}"
           admin_token: "{{ ADMIN_TOKEN }}"
           metadata_secret: "{{ METADATA_SECRET }}"
           neutron_dbpass: "{{ NEUTRON_DBPASS }}"
           neutron_server_hostname: "{{ ansible_eth0.ipv4.address}}"
           neutron_pass: "{{ NEUTRON_PASS }}"
           nova_pass: "{{ NOVA_PASS }}"

---

A complete Ansible playbook demo, which uses this role, is available on Github (openstack-ansible-galaxy/vagrant-ansible-openstack) <https://github.com/openstack-ansible-galaxy/vagrant-ansible-openstack>

---

Credits
-------
RedHat suport implemented by Abel Boldú <abel.boldu@gmx.com>


License
-------

Apache

Author Information
------------------

Davide Guerri - davide.guerri@gmail.com
