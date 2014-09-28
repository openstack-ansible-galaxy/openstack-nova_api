Nova api
=========

OpenStack Nova api service installation

_Tested on Ubuntu Precise (12.04) and Trusty (14.04)_

Requirements
------------

A RabbitMQ server. See below.

A Neutron server. See below.

A Keystone server. See below.

A Glance server. See below.

Role Variables
--------------

### Nova API (set by this role)

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `my_ip` | `{{ ansible_eth0.ipv4.address }}` | Management IP for nova-api ||
| `nova_api_hostname` | `localhost` | Hostname/IP address where this role runs, it will be used to set keystone endpoints ||
| `nova_pass` | `nova_pass_default` | Desired nova-api password ||
| `nova_port` | `8774` | Desired nova-api port ||
| `nova_protocol` | `http` | Desired nova protocol (http/https) | WiP, do not use. |

### RabbitMQ (must exist)

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `rabbit_hostname` | `localhost` | Hostname/IP address where the RabbitMQ service runs ||
| `rabbit_username` | `rabbit_username_default` | RabbitMQ username for nova ||
| `rabbit_pass` | `rabbit_pass_default` | RabbitMQ password for nova ||

### Neutron (must exist)

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `neutron_hostname` | `localhost` | Hostname/IP address where the neutron server runs ||
| `neutron_pass` | `neutron_pass_default` | Neutron admin password ||
| `neutron_port` | `9696` | Neutron port ||
| `neutron_protocol` | `http` | Neutron protocol (http/https) ||
| `metadata_secret` | `metadata_secret_default` | Metadata secret, as configured on neutron ||

### Keystone (must exist)

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `admin_token` | `admin_token_default` | Keystone service token ||
| `keystone_admin_port` | `35357` | Keystone admin port ||
| `keystone_hostname` | `localhost` | Hostname/IP address where keystone runs ||
| `keystone_port` | `5000` | Keystone port ||
| `keystone_protocol` | `http` | Keystone protocol (http/https) ||

### Glance (must exist)

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `glance_hostname` | `localhost` | Hostname/IP address where glance runs ||
| `glance_port` | `9292` | Glance port ||
| `glance_protocol` | `http` | Glance protocol (http/https) ||


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: api001
      roles:
        - role: openstack-nova_api
          rabbit_username: "openstack-nova"
          rabbit_pass: "{{ RABBIT_NOVA_PASS }}"
          admin_token: "{{ ADMIN_TOKEN }}"
          metadata_secret: "{{ METADATA_SECRET }}"
          neutron_pass: "{{ NEUTRON_PASS }}"
          nova_api_hostname: "{{ ansible_eth0.ipv4.address }}"
          nova_pass: "{{ NOVA_PASS }}"

---

A complete Ansible playbook demo, which uses this role, is available on Github (dguerri/vagrant-ansible-openstack) <https://github.com/dguerri/vagrant-ansible-openstack>

---


License
-------

Apache

Author Information
------------------

Davide Guerri - davide.guerri@gmail.com
