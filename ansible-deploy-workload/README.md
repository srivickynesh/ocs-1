# Ansible Openshift Workload Deployment

This repository contains deployment support for MongoDB, Jenkins & PGSql. It will deploy respective pod and start executing IO's on the pod.

## Prerequisites
* Host machine with Ansible Version 2.7.10 or more
* Install [jq](https://stedolan.github.io/jq/) package on oc-master node

## Deploying Pods with playbook

### Create host file
```
[oc-master]
<openshift_master_node> ansible_user=<openshift_master_node_username>   ansible_ssh_pass=<openshift_master_password>
```
For example:
```
[oc-master]
openshift.master.node.com ansible_user=ocs123 ansible_ssh_pass=password
```
### Execute playbook

```
# ansible-playbook deploy-workloads.yml -i <inventory-file-path> --tags "<pod-type>" -e count=<count> -e storage_class=<storage-class>
```
For example:
* Execute with single pod tag "mongo"
```
# ansible-playbook deploy-workloads.yml -i hosts.yaml --tags "mongo" -e count=5 -e storage_class=glusterfs-storage-block
```
* Execute with multiple pod tags "mongo,jenkins,pgsql"
```
# ansible-playbook deploy-workloads.yml -i hosts.yaml --tags "mongo,jenkins,pgsql,amq" -e count=5 -e storage_class=glusterfs-storage-block
```
