---
title: Release Notes
---

## 1.3.0

### Changes since 1.2.1

- **Syslog forwarding**: Syslogs are now streamed to the same host and port configured in Elastic Runtime settings
- **Trusty stemcells**: Server and broker are now deployed on Ubuntu “Trusty” 14.04 LTS stemcells, providing improved security, performance, and a smaller resource footprint.

### Known Issues

- Garbage collection is not yet functional. When objects are deleted, they are no longer listed for bucket contents, but they are not deleted from disk. This can lead to persistent disk filling up. Until this issue is resolved, operators should increase the persistent disk allocated to Riak CS nodes.

## 1.2.1

### Changes since 1.2.0

- **Persistence**: Data is now stored on a persistent volume.

### Known Issues

#### Upgrading from 1.2.0 to 1.2.1 is not supported

Version 1.2.1 fixes the issue with persistence in 1.2.0 by storing data files on a persistent volume. However, we will not support upgrading from 1.2.0 to 1.2.1, as data will be lost. Users of Operations Manager must uninstall (delete) the deployment of version 1.2.0 prior to deploying version 1.2.1. The following steps can be followed to migrate your bucket data, if desired:

1. Import version 1.2.1 into your Operations Manager.
1. Follow instructions in [Backing Up and Restoring](#backing-up) to back up data for all buckets.
1. Delete the deployment of Riak CS for Pivotal CF by clicking the trash can icon in Operations Manager, then Apply Changes. This will delete all service instances and bindings for the Riak CS service in Cloud Foundry and then tear down the Riak cluster.
1. Add version 1.2.1 of Riak CS for Pivotal CF to Operations Manager, then Apply Changes. This will deploy a new Riak CS cluster and restore the Riak CS service to the Cloud Foundry marketplace. For applications that used the service, new instances must be created and bound.
1. Data can be restored to these buckets by users as described in [Backing Up and Restoring](#backing-up).

## 1.2.0

### Known Issues

- Data files are stored on the ephemeral disk of the VM. If the Riak VMs are re-deployed due to a configuration change for this release in Operations Manager, data will be lost.