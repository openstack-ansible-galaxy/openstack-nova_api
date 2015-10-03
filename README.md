Nova API OpenStack Ansible Role
=========

**Status**
* [![Build Status](https://travis-ci.org/openstack-ansible-galaxy/openstack-nova_api.svg?branch=master)](https://travis-ci.org/openstack-ansible-galaxy/openstack-nova_api) on master branch
* [![Build Status](https://travis-ci.org/openstack-ansible-galaxy/openstack-nova_api.svg?branch=development)](https://travis-ci.org/openstack-ansible-galaxy/openstack-nova_api) on development branch
* [![Ansible Galaxy](http://img.shields.io/badge/dguerri-openstack--nova_api-blue.svg)](https://galaxy.ansible.com/list#/roles/1777) on Ansible Galaxy

OpenStack Nova API service installation

_Tested on Ubuntu Precise (12.04) and Trusty (14.04)_

Requirements
------------

A RabbitMQ server. See below.

A Neutron server. See below.

A Keystone server. See below.

A Glance server. See below.

For RHEL/CentOS, RHOSP or RDO repositories are needed.

Role Variables
--------------

| Name | Default value | Description |
|---  |---  |---  |
| `nova_api_database_url` | `sqlite:////var/lib/nova/nova.sqlite` | Database URI ||
| `nova_api_my_ip` | `{{ ansible_eth0.ipv4.address }}` | Management IP for nova-api |
| `nova_api_user` | `nova` | nova-api user as defined on Keystone|
| `nova_api_pass` | `nova_pass_default` | nova-api password as defined on Keystone|
| `nova_api_ec2_bind_host` | `0.0.0.0` | IP address nova-api should listen on |
| `nova_api_metadata_bind_host` | `0.0.0.0` | IP address nova-api should listen on |
| `nova_api_ec2_port` | `8773` | Desired nova-api ec2 port |
| `nova_api_port` | `8774` | Desired nova-api port |
| `nova_api_metadata_port` | `8775` | Desired nova-api metadata port |
| `nova_api_protocol` | `http` | Desired nova protocol (http/https) - WiP, do not use. |
| `neutron_hostname` | `localhost` | Hostname/IP address where the neutron server runs |
| `neutron_port` | `9696` | Neutron port |
| `neutron_protocol` | `http` | Neutron protocol (http/https) |
| `neutron_admin_username` | `neutron` | Neutron admin user |
| `neutron_pass` | `neutron_pass_default` | Neutron admin password |
| `neutron_metadata_secret` | `metadata_secret_default` | Metadata secret, as configured on neutron |
| `keystone_admin_port` | `35357` | Keystone admin port |
| `keystone_hostname` | `localhost` | Hostname/IP address where keystone runs |
| `keystone_port` | `5000` | Keystone port |
| `keystone_protocol` | `http` | Keystone protocol (http/https) |
| `glance_hostname` | `localhost` | Hostname/IP address where glance runs |
| `glance_port` | `9292` | Glance port |
| `glance_protocol` | `http` | Glance protocol (http/https) |
| `nova_api_hostname` | `localhost` | Hostname/IP address of API endpoint, used to configure nova-api. localhost is usually ok |

### RabbitMQ (must exist)

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `nova_api_rabbit_userid` | `rabbit_username_default` | RabbitMQ username for console auth ||
| `nova_api_rabbit_password` | `rabbit_pass_default` | RabbitMQ password for console auth ||
| `nova_api_rabbit_virtual_host`| `/` | RabbitMQ virtual host for console auth ||
| `nova_api_rabbit_retry_interval` | `1` | Frequency to retry connecting to RabbitMQ ||
| `nova_api_rabbit_host` | `localhost` | The RabbitMQ broker address where a single node is used ||
| `nova_api_rabbit_port` | `5672` | The RabbitMQ broker port where a single node is used ||
| `nova_api_rabbit_hosts` | `$rabbit_host:$rabbit_port` | RabbitMQ HA cluster host:port pairs ||
| `nova_api_rabbit_ha_queues` | `False` | Use HA queues in RabbitMQ (x-ha-policy: all) ||

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: api001
      roles:
        - role: openstack-nova_api
          nova_api_rabbit_userid: "openstack-nova"
          nova_api_rabbit_password: "{{ RABBIT_NOVA_PASS }}"
          keystone_admin_token: "{{ ADMIN_TOKEN }}"
          metadata_secret: "{{ METADATA_SECRET }}"
          neutron_pass: "{{ NEUTRON_PASS }}"
          nova_pass: "{{ NOVA_PASS }}"

---

A complete Ansible playbook demo, which uses this role, is available on Github (openstack-ansible-galaxy/vagrant-ansible-openstack) <https://github.com/openstack-ansible-galaxy/vagrant-ansible-openstack>

---

Credits
-------
RedHat support implemented by Abel Boldú <abel.boldu@gmx.com>

License
-------

Apache

Author Information
------------------

Davide Guerri - davide.guerri@gmail.com
