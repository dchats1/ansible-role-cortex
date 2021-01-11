Cortex
=========

Deploys a Cortex Cluster on Podman. Uses etcd as the key value store. Default storage engine is Chunks, and the role will deploy Cassandra by default. Blocks storage is also supported, but currently only works with s3 compatible object stores. If you don't have an object store I have written a separate role to deploy MinIO:
https://gitlab.com/dchats1/ansible-role-minio

For more information about Cortex:
https://cortexmetrics.io/

By adjusting the replica variables all cortex services can be scaled up. Distributors, Ingesters and Queriers can be scaled down.

Requirements
------------

This requires the containers.podman collection: https://galaxy.ansible.com/containers/podman
I recommend 1.4.0 or later.

Role Variables
--------------

Variable                            | Description
------------------------------------|------------------------------------------------------------------------
cortex_version                      | Version of Cortex to deploy. (Default: v1.6.0)
cortex_hostname                     | Hostname. (Default: cortex)
cortex_domain                       | Domain for Cortex. (Default: example.com)
cortex_manage_firewalld             | Open up nginx listen port in firewalld. (Default: false)
cortex_nginx_listen_port            | Port for Nginx to listen on. (Default: 80)
cortex_backend_podman_network       | Podman Network for backend pods and containers. (Default: podman)
cortex_frontend_podman_network      | Podman Network for frontend pods and containers. (Default: host)
cortex_base_dir                     | Base directory for cortex config and pid files. (Default: /var/lib/containers)
cortex_auth_enabled                 | Enable Authentication/Multi-tenancy. Must be quoted. (Default: 'false')
cortex_http_listen_port             | Default port for distributors to listen on. (Default: 9009)
cortex_etcd_version                 | Etcd version. (Default: v3.4.9)
cortex_etcd_replicas                | Number of etcd replicas. (Default: 3)
cortex_etcd_port                    | Etcd port. (Default: 2379)
cortex_etcd_replication_factor      | Etcd replica factor. (Default: Matches `cortex_etcd_replicas`)
cortex_ingester_replicas            | Cortex Ingester replicas. (Default: 3)
cortex_ingester_replication_factor  | Cortex Ingeseter replication factor. (Default: 3)
cortex_ingester_kvstore_provider    | Cortex Ingester KV provider. Only etcd supported right now. (Default: etcd)
cortex_ingester_kvstore_prefix      | Cortex Ingester KV prefix. (Default: collectors/)
cortex_ingesters_with_wal           | Use Ingesters with WAL. Must be enabled for blocks storage. (Default: true)
cortex_distributor_replicas         | Cortex Distributor replicas. (Default: 3)
cortex_distributor_kvstore_provider | Cortex Distributor KV provider. Only etcd supported right now. (Default: etcd)
cortex_distributor_kvstore_prefix   | Cortex Distributor KV prefix. (Default: ha-tracker/)
cortex_limits_accept_ha_samples     | Enable HA Tracker. (Default: true)
cortex_querier_replicas             | Number of Querier replicas. (Default: 2)
cortex_limits_ha_cluster_label      | Limits HA cluster label. (Default: prometheus_cluster)
cortex_limits_ha_replica_label      | Limits HA replica label. (Default: prometheus_replica)
cortex_storage_engine               | Storage engine, either chunks or blocks. (Default: chunks)
cortex_cassandra_version            | Cassandra Version. (Default: 3.11)
cortex_cassandra_replicas           | Number of Cassandra replicas. (Default: 1)
cortex_cassandra_addresses          | Cassandra addresses. These are collected dynamically from each Cassandra pod.
cortex_cassandra_keyspace           | Cortex keyspace in Cassandra. (Default: cortex)
cortex_cassandra_replication_factor | Number of replicas in Cassandra. (Default: Matches `cortex_cassandra_replicas`)
cortex_s3_bucket_name               | S3 Bucket name. (Default: cortex)
cortex_s3_endpoint                  | S3 endpoint. (Default: s3.dualstack.us-east-1.amazonaws.com)
cortex_s3_secret_access_key         | S3 Secret Access Key. (Default: secret)
cortex_s3_access_key_id             | S3 Access Key ID. (Default: secret)
cortex_s3_insecure                  | Use http for s3 endpoint. (Default: false)

Example Playbook
----------------

    - hosts: podman_host
      roles:
         - cortex

License
-------

BSD

Author Information
------------------

David Chatterton
david@davidchatterton.com
