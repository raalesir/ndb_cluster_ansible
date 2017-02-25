# ndb_cluster_ansible

The purpose is to test and play with the `NDB MySQL cluster` installation.

The goal is to make installation as automated as possible with Ansible. 

Some idead are from here: https://github.com/mdom/ansible-mysql-cluster
and at
[DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-create-a-multi-node-mysql-cluster-on-ubuntu-16-04).
The former suffer from a lot of hard-coding and repeated code, and the
latter from not being automated at all.

The present version has the followig improvements:

1. it uses more `Ansible` built'in commands rather then `Bash` instructions
2. it is follows more strictly `DRY` approach

At the moment there are just two VMs (Oracle VirtualBox + Vagrant). 
The first is for the Data Node, and the second is for cluster manager
and at the same time for the MySQL server/client.

