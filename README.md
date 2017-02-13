
**NB: this is incomplete. Don't use this for anything important**

AS7 domain
=============

CentOS 6 based JBoss AS7 cluster.

## base OS

CentOS 6.8 x64 (from https://github.com/box-cutter/centos-vm ) -
see Vagrantfile for precise version.

## requirements

* the centos base image above
* Ansible 2.x on your host machine
* Virtualbox
* Vagrant 1.8.x or better (for linked_clones)
* a Vagrant plugin (see below)

## Vagrant setup

an inventory for Vagrant is in *vagrant/hosts*, the hostnames
in there need to match your Vagrantfile.

We use the [hostmanager plugin](https://github.com/smdahlen/vagrant-hostmanager) to manage /etc/hosts and provide name resolution.

    vagrant plugin install vagrant-hostmanager

Then

    vagrant up

_NB: this will also (try to) edit your local /etc/hosts_

run the main play with:

    ansible-playbook -i vagrant/ site.yml

And you should be able to login to the DC http UI at

    http://as7dc:9990/ 

using creds in mgmt_users in roles/dc/defaults/main.yml.

If you add/destroy vagrant VMs, the 'vagrant up' should
auto-manage your local /etc/hosts along with existing VMs. If you
need to ensure it's up to date, just run

    vagrant hostmanager

## vars

* role-specific vars live in $rolename/defaults/main.yml
* 'environment' specific vars _(e.g. ansible_ssh_user)_ live in *$inventory/group_vars/all* and override role defaults

### BUGS

Oh, I expect so. Log an issue / PR if you notice any.
