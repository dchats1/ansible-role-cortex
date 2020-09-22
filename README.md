Cortex
=========

Deploys a Cortex Cluster on Podman. Uses etcd and Cassandra.
https://cortexmetrics.io/

Requirements
------------

This requires the containers.podman collection: https://galaxy.ansible.com/containers/podman

Role Variables
--------------

Variable                            | Description
------------------------------------|------------------------------------------------------------------------
cortex_version                      | Version of Cortex to deploy. (Default: v1.3.0)
cortex_single_host_deployment       | Deploy on a single host. Multi host currently not supported. (Default: true)
cortex_hostname                     | Hostname. (Default: cortex)
cortex_domain                       | Domain for Cortex. (Default: example.com)
cortex_manage_firewalld             | Open up nginx listen port in firewalld. (Default: false)
cortex_nginx_listen_port            | Port for Nginx to listen on. (Default: 80)
cortex_backend_podman_network       | Podman Network for backend pods and containers. (Default: podman)
cortex_frontend_podman_network      | Podman Network for frontend pods and containers. (Default: host)
cortex_base_dir                     | Base directory for cortex config and pid files. (Default: /var/lib/containers)
cortex_http_listen_port             | Default port for distributors to listen on. (Default: 9009)
cortex_etcd_version                 | Etcd version. (Default: v3.4.9)
cortex_etcd_replicas                | Number of etcd replicas. (Default: 3)
cortex_etcd_port                    | Etcd port. (Default: 2379)
cortex_etcd_replication_factor      | Etcd replica factor. (Default: Matches `cortex_etcd_replicas`)
cortex_ingester_replicas            | Cortex Ingester replicas. (Default: 3)
cortex_ingester_kvstore_provider    | Cortex Ingester KV provider. Only etcd supported right now. (Default: etcd)
cortex_ingester_kvstore_prefix      | Cortex Ingester KV prefix. (Default: collectors/)
cortex_ingesters_with_wal           | Use Ingesters with WAL. (Default: true)
cortex_distributor_replicas         | Cortex Distributor replicas. (Default: 3)
cortex_distributor_kvstore_provider | Cortex Distributor KV provider. Only etcd supported right now. (Default: etcd)
cortex_distributor_kvstore_prefix   | Cortex Distributor KV prefix. (Default: ha-tracker/)
cortex_limits_accept_ha_samples     | Enable HA Tracker. (Default: true)
cortex_querier_replicas             | Number of Querier replicas. Currently only 1 supported. (Default: 1)
cortex_limits_ha_cluster_label      | Limits HA cluster label. (Default: prometheus_cluster)
cortex_limits_ha_replica_label      | Limits HA replica label. (Default: prometheus_replica)
cortex_cassandra_version            | Cassandra Version. (Default: 3.11)
cortex_cassandra_replicas           | Number of Cassandra replicas. (Default: 1)
cortex_cassandra_addresses          | Cassandra addresses. These are collected dynamically from each Cassandra pod.
cortex_cassandra_keyspace           | Cortex keyspace in Cassandra. (Default: cortex)
cortex_cassandra_replication_factor | Number of replicas in Cassandra. (Default: Matches `cortex_cassandra_replicas`)

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: cortex
      roles:
         - cortex

License
-------

BSD

Author Information
------------------

David Chatterton
david@davidchatterton.com
