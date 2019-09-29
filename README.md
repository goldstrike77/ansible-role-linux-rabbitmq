![](https://img.shields.io/badge/Ansible-RabbitMQ-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_rabbitmq.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [RabbitMQ Versions](#RabbitMQ-versions)
- [ Role variables](#Role-variables)
  * [Main Configuration](#Main-parameters)
  * [Other Configuration](#Other-parameters)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Hosts inventory file](#Hosts-inventory-file)
  * [Vars in role configuration](#vars-in-role-configuration)
  * [Combination of group vars and playbook](#combination-of-group-vars-and-playbook)
- [License](#license)
- [Author Information](#author-information)
- [Contributors](#Contributors)

## Overview
This Ansible role installs RabbitMQ on linux operating system, including establishing a filesystem structure and server configuration with some common operational features.

## Requirements
### Operating systems
This role will work on the following operating systems:

  * CentOS 7

### RabbitMQ versions

The following list of supported the RabbitMQ releases:

  * RabbitMQ 3.7+

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `rabbitmq_is_install`: A boolean value, whether install the RabbitMQ.
* `rabbitmq_version`: Specify the RabbitMQ version.
* `rabbitmq_path`: Specify the RabbitMQ data directory.

##### System Variables
* `rabbitmq_channel_max`: Define the max permissible number of channels per connection.
* `rabbitmq_frame_max`: Define the max permissible size of an AMQP frame in bytes.
* `rabbitmq_handshake_timeout`: Maximum amount of time allowed for the handshake.
* `rabbitmq_heartbeat`: Heartbeat interval in seconds.
* `rabbitmq_tcp_listen_options_backlog`: Connection Backlog.
* `rabbitmq_vm_memory_high_watermark_absolute`: Define an absolute limit of RAM used by the node.
* `rabbitmq_vm_memory_high_watermark_paging_ratio`: Configuring the Paging Threshold.
* `rabbitmq_vm_memory_high_watermark_relative`: Define the memory threshold at which the flow control is triggered can be adjusted.

##### Service Mesh
* `environments`: Define the service environment.
* `tags`: Define the service custom label.
* `exporter_is_install`: Whether to install prometheus exporter.
* `consul_public_register`: false Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_clients`: List of public consul clients.
* `consul_public_http_port`: The consul HTTP API port.

### Other parameters
There are some variables in vars/main.yml:

## Dependencies
- Ansible versions > 2.8 are supported.

## Example

### Hosts inventory file
See tests/inventory for an example.

    node01 ansible_host='192.168.1.10' rabbitmq_version='3.7'

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - role: ansible-role-linux-rabbitmq
           rabbitmq_version: '3.7'

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`

    rabbitmq_version: '3.7'
    rabbitmq_path: '/data'
    rabbitmq_port:
      epmd: '4369'
      erlang_dist_client: '35672-35682'
      erlang_dist_server: '25672'
      exporter: '9419'
      http: '15672'
      ssl: '5671'
      tcp: '5672'
    rabbitmq_channel_max: '128'
    rabbitmq_frame_max: '131072'
    rabbitmq_handshake_timeout: '10000'
    rabbitmq_heartbeat: '60'
    rabbitmq_tcp_listen_options_backlog: '4096'
    rabbitmq_vm_memory_high_watermark_absolute: '2GB'
    rabbitmq_vm_memory_high_watermark_paging_ratio: '0.5'
    rabbitmq_vm_memory_high_watermark_relative: '0.4'
    rabbitmq_bu_arg:
      - vhost: '/'
        user: 'example'
        pass: 'changeme'
        read_priv: '.*'
        write_priv: '.*'
        configure_priv: '.*'
        tags: 'example'
    environments: 'SIT'
    tags:
      subscription: 'default'
      owner: 'nobody'
      department: 'Infrastructure'
      organization: 'The Company'
      region: 'IDC01'
    exporter_is_install: false
    consul_public_register: false
    consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
    consul_public_clients: 'localhost'
    consul_public_http_port: '8500'

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
