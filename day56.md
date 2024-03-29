---
title: "Understanding Ad-hoc commands in Ansible"
datePublished: Thu Dec 28 2023 09:29:33 GMT+0000 (Coordinated Universal Time)
cuid: clqp07489000608gv2tseb2tq
slug: understanding-ad-hoc-commands-in-ansible
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703755512303/f707d837-1266-42d9-8111-25a4418f0a49.png
tags: aws, ansible, 90daysofdevops

---

Ansible ad hoc commands are one-liners designed to achieve a very specific task they are like quick snippets and your compact swiss army knife when you want to do a quick task across multiple machines.

To put simply, Ansible ad hoc commands are one-liner Linux shell commands and playbooks are like a shell script, a collective of many commands with logic.

Ansible ad hoc commands come handy when you want to perform a quick task.

# Task-01

* ### **Write an ansible ad hoc ping command to ping 2 servers from inventory file**
    

```ini
ansible server1:server2 -m ping
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703750088329/d177c6c7-670a-4bef-86d8-5a24665e9b1e.png align="center")

* ### **Write an ansible ad hoc command to check uptime**
    

```ini
ansible -i /path/to/inventory/file all -m command -a uptime
```

If your inventory is in the default location (/etc/ansible/hosts or ~/.ansible.cfg) you can omit the -i option and the path altogether.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703750352328/ab351e11-2eb6-41e5-bb78-da5a26f9a4d1.png align="center")

* ### Ansible ad hoc command to check the amount of free memory or the amount of memory used by hosts.
    

```ini
ansible all -a "free -m"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703751595044/73333601-fc32-4bdd-8bac-c88f70014b1a.png align="center")

* ### Ansible ad hoc command to get physical memory allocated to the host
    

```ini
ansible all -m shell -a "cat /proc/meminfo|head -2"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703751884866/a5a8eace-5a31-4999-9671-c3aa6fc2866b.png align="center")

* ### Ansible command to check the disk space on all hosts in an inventory file
    

```ini
ansible all -m shell -a 'df -hT'
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703752596877/30da6161-e472-436a-8a84-14225b4aa5c4.png align="center")

### Ansible command to list all the running processes on a specific host in an inventory file

```ini
ansible all -m shell -a "ps aux"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703752714840/ed78a32a-e64c-4230-b2de-4f59597ab0eb.png align="center")

### Ansible command to run a shell command with sudo on all hosts in an inventory file

```ini
ansible all -m shell -a "sudo apt-get update" 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703752880529/96e58ef6-5399-4a3b-bbc0-627d6c70fbc9.png align="center")

### Ansible command to show all 2 servers’ python versions.

```ini
ansible all -m shell -a "sudo python3 --version"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703753054072/4f153336-1d36-475a-af47-9fb5501751e0.png align="center")

### Ansible command to check the status of a specific service on all hosts in an inventory file

```ini
ansible all -m service -a "name=apache"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703753319632/27931330-3900-42c2-8848-ac32d5c99a84.png align="center")

The following ad hoc command with copy module copies the file from Src location on the local control machine to the specified location on the remote server

```ini
ansible -i inventory_file all -m copy -a 'src=/local/path/to/file dest=/remote/path/to/file mode=0644'
```

First create a simple text file at any location, here create a text file at /home/ubuntu location with name file.txt.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703754069404/55cb5e02-e857-4124-aa82-798e95ce6fd3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703754087597/012c6563-a650-45e7-a4cf-44ce058c22ff.png align="center")

Check if the file is successfully copied to all the servers with the ‘sudo ls command’

```ini
ansible all -m shell -a 'sudo ls /home/ubuntu'
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703754577533/eee527bf-7c35-4d1b-a4d7-ff352b37be84.png align="center")

### Create a file with 755 permission using ansible ad hoc commands

```ini
ansible all -m file -a "path=/home/ubuntu/ansible state=directory mode=0755" -b
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703754740128/1c6ad3d9-2d33-4c98-84cd-7c038adc6461.png align="center")
