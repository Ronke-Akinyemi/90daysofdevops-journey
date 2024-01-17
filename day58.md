---
title: "Ansible Playbooks"
datePublished: Fri Dec 29 2023 17:58:50 GMT+0000 (Coordinated Universal Time)
cuid: clqqxtxd9000108l73ocpex36
slug: ansible-playbooks
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703872359167/c2d746f1-a34e-4f59-9132-0ec2c07b6d91.png
tags: aws, 90daysofdevops, ansible-playbook

---

Ansible playbooks run multiple tasks, assign roles, and define configurations, deployment steps, and variables. If you’re using multiple servers, Ansible playbooks organize the steps between the assembled machines or servers and get them organized and running in the way the users need them to. Consider playbooks as the equivalent of instruction manuals.

# Task-01

* Write an ansible playbook to create a file on a different server
    
* Write an ansible playbook to create a new user.
    
* Write an ansible playbook to install docker on a group of servers
    

### Ansible playbook to create a file on a different server

Create a file named create\_file.yml . Use the `vim create_file.yml` command.

```ini
---
- name: create a file
  hosts: all
  become: yes

  tasks:
    - name: create a new file
      file:
        path: /home/ubuntu/demo.txt
        state: touch
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703865282002/d0171037-22f2-4923-b07e-7c403bbef40b.png align="center")

Run the playbook with `ansible-playbook create_file.yml` command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703865363172/05a38727-15e6-45e2-a99e-01f200f4e16a.png align="center")

Verify that the file has been successfully created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703865500963/bb063e10-98b0-4539-ab24-e743c2cd6f9e.png align="center")

### Ansible playbook to create a new user

Create a file named create\_user.yml . Use the `vim create_user.yml` command.

```ini
---
- name: create a user using ansible playbook
  hosts: all
  become: yes

  tasks:
    - name: create a user
      user:
        name: ronke
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703865831530/4174acaa-9777-43c4-b986-b857fa85ae5d.png align="center")

Run the playbook with `ansible-playbook create_user.yml` command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703865915505/b2db35e4-8efa-40a3-b667-246a5c51b9ff.png align="center")

Verify that the user has been successfully created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703866028533/79204493-5c20-4f70-a2e5-f74dc0e4545a.png align="center")

### Ansible playbook to install docker on a group of servers

Create a file named install\_docker.yml . Use the `vim docker_install.yml` command.

```ini
---
- name: Install Docker on a group of servers
  hosts: all
  become: yes
  tasks:
    - name: Add Docker GPG apt Key
      apt_key:
        url: https://download.docker.com/linux/ubuntu/gpg
        state: present

    - name: Add Docker Repository
      apt_repository:
        repo: deb https://download.docker.com/linux/ubuntu focal stable
        state: present

    - name: Install Docker
      apt:
        name: docker-ce
        state: latest
```

Run the playbook with `ansible-playbook create_user.yml` command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703866234988/fbf66caf-771e-4c63-a93d-59fea7ac039c.png align="center")

Verify Docker installation.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703866310056/6f3cc8b7-52d7-44a8-b24b-cf9191c860ff.png align="center")

### Writing ansible playbooks with the best practices.

1. **Naming:** Use meaningful and descriptive names for roles, tasks, and variables for easy identification and understanding.
    
2. **Use YAML Syntax Properly:** Follow consistent indentation rules using spaces or tabs for readability. For easy comprehension, use clear and descriptive names for playbooks, roles, tasks, and variables.
    
3. **Organize Playbooks and Roles:** Structure playbooks logically into distinct sections for clear understanding. Divide tasks into roles based on functionality or purpose for code reusability. Utilize directories like tasks, handlers, templates, and vars within roles for better organization.
    
4. **Idempotency:** Ensure your playbooks are idempotent, meaning they can be executed multiple times without causing unintended or irreversible changes. Utilize Ansible modules and tasks that support idempotent operations, such as modifying configurations without introducing inconsistencies or disrupting existing states.
    
5. **Variable Usage:** Define variables in separate YAML files for better organization and management. Use meaningful variable names for enhanced code readability and understanding.
