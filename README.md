
**NB: this is rough as badgers. don't use this for anything important**

AS7 domain
=============

CentOS 6 based JBoss AS7 cluster.

## base OS

CentOS 6.7 x64 (from https://github.com/box-cutter/centos-vm ) -
see Vagrantfile for precise version.

## requirements

* the centos base image above
* Ansible 1.9 on your host machine
* Virtualbox
* Vagrant 1.8.x or better (for linked_clones)
* a Vagrant plugin (see below)

## assumptions

* Hosts permit passwordless ssh+sudo for the relevant ansible_ssh_user.
* hosts connect to each others inventory hostname
* name lookups work (see previous point)

## Vagrant setup

an inventory for Vagrant is in *vagrant/hosts*, the hostnames
in there need to match your Vagrantfile.

We'll need name resolution, and /etc/hosts is nice and simple.

The [hostmanager plugin](https://github.com/smdahlen/vagrant-hostmanager) will auto-manage that.

    vagrant plugin install vagrant-hostmanager

Then

    vagrant up

_NB: this will also (try to) edit your local /etc/hosts_

run the main play with:

    ansible-playbook -i vagrant/ site.yml

If you add/destroy vagrant VMs, the 'vagrant up' should
auto-manage your local /etc/hosts along with existing VMs. If you
need to ensure it's up to date, just run

    vagrant hostmanager

## vars

* role-specific vars live in $rolename/defaults/main.yml
* 'environment' specific vars _(e.g. ansible_ssh_user)_ live in [all:vars] within the relevant inventory
  and override role defaults

### BUGS

Oh, I expect so. Log an issue / PR if you notice any.
