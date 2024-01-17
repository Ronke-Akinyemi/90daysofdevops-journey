---
title: "Ansible Project"
datePublished: Sat Dec 30 2023 05:38:39 GMT+0000 (Coordinated Universal Time)
cuid: clqrmtw76000408l6f7pte8yp
slug: ansible-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703914417604/dc3e18ee-9dd0-45d9-9849-8098ce397c0b.png
tags: aws, ansible, 90daysofdevops

---

Ansible playbooks are amazing, as you learned yesterday. What if you deploy a simple web app using ansible, sounds like a good project, right?

# Task-01

* Create 3 EC2 instances . Make sure all three are created with same key pair
    

Launch 3 EC2 Instances with the same Private key pair, one will be the Ansible master and the remaining two will be nodes ( Ansible\_Node1 and Ansible\_Node2).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703907392289/8b8c8a6f-8e30-4c43-99fb-cc90cd48db31.png align="center")

* Install Ansible in host server
    

Connect to Your EC2 Instance using SSH

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703908202074/fec2c13e-0a5e-491f-99ea-3973b46a2510.png align="center")

Add the Ansible PPA (Personal Package Archive) to your instance

```ini
sudo apt-add-repository ppa:ansible/ansible
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703908633777/0b1b39e4-7e96-491b-b5b2-99d6c74f8b3f.png align="center")

Update System Packages

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703908703957/04636e40-9b62-4a9c-b5af-52a341130bb0.png align="center")

Install Ansible

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703908776566/1b9771d5-0c35-4ca8-8393-bd26a7077393.png align="center")

Verify Ansible Installation

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703908965838/abde66c9-dfc0-4c99-b8ce-06a5450d14b4.png align="center")

* Copy the private key from local to Host server (Ansible\_host) at (/home/ubuntu/.ssh)
    

Now, copy the private key pair from the local to the host server (Ansible master) at `/home/ubuntu/.ssh` and paste the private key in the file

Copy the private key from your local.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703909826756/352ee9b9-d88c-4aaa-b188-9f6a4e150be6.png align="center")

Give permissions to the private key file using chmod command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703909997013/9bf6b2dc-43e0-4bad-8717-1947688f31a6.png align="center")

* Access the inventory file using **sudo vim /etc/ansible/hosts**
    

Create inventory file at location **/etc/ansible/hosts** which is by default location of the file. An Ansible hosts file is a configuration file that contains a list of hosts or servers. Add the IP addresses of the servers and also add private key file locations to use for authentication.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703910554641/b681e160-9701-4a2e-be1d-44540e54ec71.png align="center")

Use `ansible-inventory --list -y` to check the list of hosts

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703910601781/d6109300-4c63-4a4d-96e6-5f9e7d65931e.png align="center")

* Create a playbook to install Nginx
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703911266950/32009b92-f230-400f-8b98-4f0bc11a2bfe.png align="center")

Run the playbook using ansible-playbook command.

```ini
ansible-playbook file-name.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703911680550/3562b44e-382c-4a84-9387-9d6cb2b4d99b.png align="center")

* Deploy a sample webpage using the ansible playbook
    

Create a new file index.html in the playbook directory, and add some content

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703911971337/a291e9c5-30cf-42ed-9253-b412b6f1077a.png align="center")

Update the Ansible playbook file `install_nginx.yml` in the playbook directory by providing the index.html file path, and the destination will be the default Nginx web server document root directory at /var/www/html/.

```ini
---
- name: playbook to install Nginx and deploy sample webpage
  hosts: all
  become: yes

  tasks:
    - name: Update apt package cache
      apt:
        update_cache: yes

    - name: Install Nginx
      apt:
        name: nginx
        state: latest

    - name: Start Nginx 
      service:
        name: nginx
        state: started

    - name: Deploy a sample webpage
      copy:
        src: /home/ubuntu/index.html
        dest: /var/www/html/
      become: true
      become_user: root
      become_method: sudo
```

This playbook will copy the index.html file to the default Nginx web server document root directory at /var/www/html/.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703913391865/64a14452-005e-411b-a040-df8ac0a224b7.png align="center")

After successfully running the Ansible playbook, launch a web browser and navigate to the public IP address of any of the EC2 instances where Nginx is running.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703914059321/71ed0fbc-92ed-441b-8c72-9c25ceb4b1fb.png align="center")

Server1

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703914085727/db039aa6-09d4-4e26-96e3-a9bb05edb8f1.png align="center")

Server2

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703914116972/08047a45-a3ad-4f6e-b237-5df3d9ae28a9.png align="center")
