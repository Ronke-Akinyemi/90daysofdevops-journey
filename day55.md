---
title: "Understanding Configuration Management with Ansible"
datePublished: Tue Dec 26 2023 20:23:56 GMT+0000 (Coordinated Universal Time)
cuid: clqmsoy9k000008jk94w02z9a
slug: understanding-configuration-management-with-ansible
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703620029879/b345a373-0435-4531-97dc-02091363ddcc.png
tags: aws, ansible, devops-articles

---

## What's this Ansible?

Ansible is an open-source automation tool or platform used for IT tasks such as configuration management, application deployment, intraservice orchestration, and provisioning.

# Task-01

* Installation of Ansible on AWS EC2 (Master Node) `sudo apt-add-repository ppa:ansible/ansible` `sudo apt update` `sudo apt install ansible`
    

**Launch an EC2 Instance**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703613487895/73b05e5f-9680-4464-b63f-7234f805fcd2.png align="center")

**Connect to Your EC2 Instance:** Use an SSH client like `ssh` to connect to your AWS EC2 instance

```bash
ssh -i your-key.pem ubuntu@your-instance-ip
```

**Add the Ansible PPA (Personal Package Archive) to your instance**

```bash
sudo apt-add-repository ppa:ansible/ansible
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703614079943/cee91b0b-a568-4104-a2d5-3105a6034c94.png align="center")

**Update System Packages:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703614211670/06fc3222-cc7e-45f9-a8a8-508f3cbf930c.png align="center")

**Install Ansible:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703614277213/01d61ae5-e4c8-4054-aa1f-333ff93bc560.png align="center")

**Verify Ansible Installation:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703614366050/875e44aa-87cb-4db7-b368-e795e22529ac.png align="center")

# Task-02

* read more about Hosts file `sudo nano /etc/ansible/hosts ansible-inventory --list -y`
    

### **Ansible Inventory File (**`/etc/ansible/hosts`):

The Ansible hosts file is a critical component that defines the hosts (machines or servers) that Ansible will manage. This file is used to specify inventory details, such as hostnames, IP addresses, connection details, and groups of hosts. The default location for the hosts file is usually `/etc/ansible/hosts`, but you can use other files and directories as well.

The hosts file uses an INI-style format. Each host or group of hosts is specified under a section header, and the properties for each host are listed below the header.

Example:

```ini
[web_servers]
web1 ansible_host=192.168.1.101 ansible_user=ubuntu
web2 ansible_host=192.168.1.102 ansible_user=ubuntu

[db_servers]
db1 ansible_host=192.168.1.201 ansible_user=ubuntu
db2 ansible_host=192.168.1.202 ansible_user=ubuntu
```

In this example:

* `web_servers` and `db_servers` are group names.
    
* `ansible_host` specifies the IP address of the host.
    
* `ansible_user` specifies the SSH username used to connect to the host.
    

### **To List Inventory:**

```ini
ansible-inventory --list -y
```

This command displays the entire inventory in YAML format. It can be useful to check if your inventory file is correctly configured and if Ansible is able to recognize the hosts.

# Task-03

* Setup 2 more EC2 instances with same Private keys as the previous instance (Node)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703615979764/978bd362-3eed-42f9-a7d7-be2651873941.png align="center")

* Copy the private key to master server where Ansible is setup
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703616425798/7fbe0566-45c0-4a02-9a42-267f291c354c.png align="center")

Then use then `chmod` command to grant the crucial file permission

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703616878643/f0597a8a-6d62-44f7-8900-314b3c12d1c9.png align="center")

**Use** `sudo vim /etc/ansible/hosts` to add the IP addresses of the servers and the location of the private key file to be used for authentication.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703617284786/005bbcbc-1761-4afd-bda3-ee7217ae91e0.png align="center")

Use `ansible-inventory --list -y` to check the list of hosts

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703617502298/2c5ee66e-9b30-4a6a-ab8d-0c002ebe3960.png align="center")

* Try a ping command using ansible to the Nodes.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703617596179/8d475a0d-536a-43bd-8614-0760210530f2.png align="center")
