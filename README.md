# ansible-mesos

Ansible playbooks for setting-up and maintaining a fully-functionaly [Mesos](http://mesos.apache.org/) cluster.

Includes:

* Zookeeper
* Mesos master
* Mesos slave
* Mesos dns
* Marathon
* Docker

and all of their dependencies. You can run everything in one box, or have a highly-available setup with every component running on its own server with multiple masters/zookeepers (just edit `inventories/production/inventory`).

## Requirements

* [Ansible](http://www.ansible.com/) – `$ brew update; brew install ansible`
* [Vagrant](https://www.vagrantup.com/)
* [Vagrant-cachier plugin](https://github.com/fgrehm/vagrant-cachier) – `$ vagrant plugin install vagrant-cachier` (optional but recommended)

## Test

Run everything in a single virtual machine:

```bash
$ vagrant up
$ vagrant ssh

# re-apply changes:
$ vagrant provision
```

## Production

#### 1. Add new server

Replace `TODO`s in `new-server.yml` with your own passwords as instructed. When a new server is added to the cluster, insert it to `inventories/production/inventory` and run (ubuntu trusty64 14.04 expected):

```bash
# configure all servers
$ ansible-playbook -i inventories/production new-server.yml

# or configure single server:
$ ansible-playbook -i inventories/production -l <new-server-host> new-server.yml
```

#### 2. Run ansible

```bash
$ ansible-playbook -i inventories/production site.yml
```
