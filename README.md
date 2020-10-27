# Apache ZooKeeper

Ansible role for installing and configuring Apache ZooKeeper on ubuntu 18.04-lts.

This role can be used to install and cluster multiple ZooKeeper nodes, this uses
all hosts defined for the "zookeeper-nodes" group in the inventory file by
default. All servers are added to the zoo.cfg file along with the leader and
election ports.

## Requirements

Platform: ubuntu 18.04-lts

Java: Java 8

## Role Variables

---
zookeeper_mirror: https://downloads.apache.org/zookeeper/stable
zookeeper_version: 3.5.8
zookeeper_package: apache-zookeeper-{{ zookeeper_version }}-bin.tar.gz

zookeeper_group: zookeeper
zookeeper_user: zookeeper

zookeeper_root_dir: /usr/share
zookeeper_install_dir: '{{ zookeeper_root_dir }}/apache-zookeeper-{{ zookeeper_version }}'

zookeeper_dir: '{{ zookeeper_root_dir }}/zookeeper'
zookeeper_log_dir: /var/log/zookeeper

zookeeper_data_dir: /var/lib/zookeeper
zookeeper_data_log_dir: /var/lib/zookeeper
zookeeper_client_port: 2181

zookeeper_id: 1

zookeeper_leader_port: 2888
zookeeper_election_port: 3888

zookeeper_servers: "{{groups['zookeeper-nodes']}}"
zookeeper_environment: {}


### Default Ports

| Port | Description                         |
| ---- | ----------------------------------- |
| 2181 | Client connection port              |
| 2888 | Quorum port for clustering          |
| 3888 | Leader election port for clustering |

### Default Directories and Files

| Description                                | Directory / File                            |
| ------------------------------------------ | ------------------------------------------- |
| Installation directory                     | `/usr/share/apache-zookeeper-<version>`     |
| Symlink to install directory               | `/usr/share/zookeeper`                      |
| Symlink to configuration                   | `/etc/zookeeper/zoo.cfg`                    |
| Log files                                  | `/var/log/zookeeper`                        |
| Data directory for snapshots and myid file | `/var/lib/zookeeper`                        |
| Data directory for transaction log files   | `/var/lib/zookeeper`                        |
| Systemd service                            | `/usr/lib/systemd/system/zookeeper.service` |
| System Defaults                            | `/etc/default/zookeeper`                    |

## Starting and Stopping ZooKeeper services

- The ZooKeeper service can be started via: `systemctl start zookeeper`
- The ZooKeeper service can be stopped via: `systemctl stop zookeeper`

## Dependencies

No dependencies

## Deploying ansible-playbook

````
ansible-playbook -i inventory main.yml -vvv
````

## License

ilyes Ajroud