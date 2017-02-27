# ndb_cluster_ansible

The purpose is to test and play with the `NDB MySQL cluster` installation.

The goal is to make installation as automated as possible with Ansible. 
Tested on:
```
❯ vagrant --version
Vagrant 1.9.1`
❯ VirtualBox --help
Oracle VM VirtualBox Manager 5.1.14
```

Some ideas are from here: https://github.com/mdom/ansible-mysql-cluster
and at
[DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-create-a-multi-node-mysql-cluster-on-ubuntu-16-04).
The former suffer from a lot of hard-coding and repeated code, and the
latter from not being automated at all. Another source of information is the
offcial instructions:
https://dev.mysql.com/doc/refman/5.6/en/mysql-cluster.html

The present version has the following improvements:

1. it uses more `Ansible` built'in commands rather then `Bash` instructions
2. it is follows more strictly the `DRY` approach




Thing like
`config.ssh.insert_key = false` in the Vagrantfile doesn't work for me for a some
reason. So i generated key-pair in the `Vagrantfile` directory and
use `Ansible` task to deliver *both* parts to the `$HOME/.ssh/` on each host.



|Node	| IP Address|
--------|-----------|
|Management node (mgmd)	|192.168.1.10|
|SQL node (mysqld)	|192.168.1.13|
|Data node1 (ndbd)	|192.168.1.11|
|Data node2 (ndbd)	|192.168.1.12|

After cloning the repo, the source directory (the one with the `Vagrantfile)`
should look like:
```
 ❯ tree -L 2                                                                                [12:21:42]
.
├── README.md
├── Vagrantfile
├── group_vars
│   └── all
├── id_rsa
├── id_rsa.pub
├── mysql_servers.yml
├── roles
│   ├── common
│   ├── mysql_cluster_common
│   ├── mysql_cluster_data
│   ├── mysql_cluster_mgm
│   └── mysql_cluster_sql
├── site.yml
├── staging
```
The keys `id_rsa` and `id_rsa.pub` must be created by the user.

The the best case scenario it is enough to issue:
```
vagrant up --provision
```

Instructions for other cases are to be created :)
And the repo in general must be improved...