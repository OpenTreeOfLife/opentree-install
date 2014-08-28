# OpenTreeOfLife
This project contains [Ansible](http://www.ansible.com/) playbooks for [OpenTreeOfLife](http://blog.opentreeoflife.org/) project.
This script is created by Temi Varghese by incorporating ideas from [ala-install](https://github.com/AtlasOfLivingAustralia/ala-install)

## Setup the OpenTreeOfLife demo

Below are some instructions for setting up the [OpenTreeOfLife](http://blog.opentreeoflife.org/) demo with Ansible & Vagrant on your local machine.

#### 1. Vagrant
[Vagrant](http://www.vagrantup.com) can be used to test ansible playbooks on your local machine. To use this, you will need to install
[VirtualBox](https://www.virtualbox.org) and [Vagrant](http://www.vagrantup.com).
```vagrant/ubuntu``` contain configurations that can used with [VirtualBox](https://www.virtualbox.org/) to bring up a VH for deploying against.
This is included only to simplify local testing, but any server running Ubuntu 12.x could be used.

To create a virtual machine with vagrant:

```
$ cd vagrant/ubuntu
$ vagrant up
```

The first execution of this downloads the Ubuntu image which can take some time due to the size of image. Once ready you can ssh to your VM like so:

```
$ ssh vagrant@10.1.1.2
```

with password ```vagrant```.

or

```
$ ssh root@10.1.1.2 -i ~/.vagrant.d/insecure_private_key
```

with user name root and without password

#### 2. Ansible

## Download ansible
Ansible is available on [github](https://github.com/ansible/ansible).

```
cd ~
git clone https://github.com/ansible/ansible
cd ~/ansible
source hacking/env-setup
```
The last step above sets environmental variables into your shell instance.

To run Ansible against your vagrant instance you need to locate the correct key file (e.g. the default insecure vagrant file if using the Vagrant config for testing):

```
$ cd ~/opentree-install/ansible
$ ansible-playbook -i inventories/opentreeDemo opentree.yml --private-key ~/.vagrant.d/insecure_private_key  -u root
```

## Notes for different environments

There are some minor differences for running these playbooks against Nectar VMs, CSIRO IM&T VMs and Vagrant VMs.
In each case you will need to create an inventory file that points to your VM(s).

For VMs:
```
$ ansible-playbook -i inventories/opentreeDemo opentree.yml --private-key <PATH_TO_YOUR_PEM_FILE>  -u root
```

#### Open Tree demo sites

```
http://10.1.1.2:8000/curator
http://10.1.1.2:8000/opentree
http://10.1.1.2:7474/webadmin - treemachine
http://10.1.1.2:7476/webadmin - taxomachine
http://10.1.1.2:7478/webadmin - oti
```