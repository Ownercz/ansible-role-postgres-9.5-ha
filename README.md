# ansible-role-postgres-9.5-ha
Ansible role for PostgreSQL 9.5 High Avaiability master-slave replication on Centos 7.
## Supported platforms
* Centos 7
* PostgreSQL 9.5

## Running the role


```
---
- name: Setup PostgreSQL enviroment
  hosts: dev
  roles:
      - ansible-role-postgres-9.5-ha
  vars:
   - pgsql_95_data_directory: /var/lib/pgsql/9.5/data/
   - pgsql_95_main_directory: /var/lib/pgsql/9.5/main/
   - pgsql_replication_user: replicationusr
   - pgsql_replication_password: 3aa6d96cea
   - pgsql_users:
      - entry: "host   all             all               0.0.0.0/0                 trust"
        description: "#Enable all"
      - entry: "host   replication             all               0.0.0.0/0                 trust"
        description: "#Enable all"
   - wal_level: "wal_level = hot_standby"
   - archive_mode: "archive_mode = on"
   - archive_cmd: "archive_command = 'test ! -f /opt/pgsql/archivedir/%f && cp %p /opt/pgsql/archivedir/%f'"
   - max_wal_senders: "max_wal_senders = 3"
   - hot_standby: "hot_standby = on"
   - recovery_standby: "standby_mode = on"
   - master_connection: "primary_conninfo = 'host=192.168.1.175 port=5432 user=replicationusr'"
   - trigger_file_location: "trigger_file = '/opt/trigger/turnnow'"
   - slavnuke: true
   - listen: "listen_addresses = '*'"
   - ha_directory: "/opt/hapgsql"
   - ip_mgmt_01: "192.168.1.167"
   - ip_mgmt_02: "192.168.1.168"
   - gateway: "192.168.1.1"
   - ip_clear: "127.0.0.1"
   - firstrun_adapter: "Wired connection 1"
   - ip_master: "192.168.1.175"
   - ip_slave: "192.168.1.176"
   - ens_dev: "ens224"
   - ens_mgmt: "ens192"

```