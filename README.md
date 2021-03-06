Cluster-ansible-aio
===================

Multi-node deployment of cluster apps (Kolla, oVirt, RKE, OpenShift, GlusterFS) on a single host, using heavily Libvirt, Docker and Ansible.

![cluster-ansible-aio](https://user-images.githubusercontent.com/9655027/31175714-6e453b1e-a910-11e7-8a60-f7c6d2114b1a.png)

Cluster-ansible-aio is an open source tool for automating deployment of cluster apps (oVirt, RKE, Kolla, GlusterFS, OpenShift,...), on a single physical machine.

-   Source: <https://github.com/blallau/cluster-ansible-aio>

Features
--------

-   Multi-nodes (N master and N worker)
-   Multi OS (CentOS and Ubuntu compliancy)
-   Multi Networks (DHCP, static)
-   Multi block storage (LVM disks)
-   Heavily automated using Ansible
-   Quick deployment: using PIP cache proxy (Devpi) and APT cache proxy (apt-cacher-ng)

Quickstart guide
----------------

Install dependencies
--------------------

Make sure the PIP package manager is installed and upgraded to the latest version:

```
#CentOS
sudo yum install epel-release
sudo yum install python-pip
sudo pip install -U pip

#Ubuntu
sudo apt-get update
sudo apt-get install python-pip
sudo pip install -U pip
```

Install dependencies needed to build the code with PIP package manager:

```
#CentOS
sudo yum install python-devel libffi-devel gcc openssl-devel libselinux-python

#Ubuntu
sudo apt-get install python-dev libffi-dev gcc libssl-dev python-selinux
```

Install Ansible (>= 2.6) using PIP:

```
#CentOS & Ubuntu
sudo pip install -U ansible
```

Cluster Deployment
------------------

1. Clone cluster-ansible-aio.

Command:

    git clone https://github.com/blallau/cluster-ansible-aio
    cd cluster-ansible-aio

2. Bootstrap hypervisor, Docker registry, proxies (PIP and APT), and create
virtual nodes.

By default, virtual nodes OS will be same as hypervisor OS.

    ./cluster-ansible-aio create-virtual-nodes

3. [Bootstrap all virtual nodes (install packages, configure Docker,
configure SSH...).]

Command:

    ./cluster-ansible-aio nodes-bootstrap

4. [Bootstrap Docker in virtual nodes.]

Command:

    ./cluster-ansible-aio docker-bootstrap

Clean-up
--------

1. Clean-up hypervisor and remove virtual nodes.

    ./cluster-ansible-aio remove-virtual-nodes --yes-i-really-really-mean-it
