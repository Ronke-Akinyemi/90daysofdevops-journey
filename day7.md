---
title: "Understanding package manager and systemctl"
datePublished: Fri Oct 20 2023 21:38:06 GMT+0000 (Coordinated Universal Time)
cuid: clnz4u9mw000609l57tgu2xyq
slug: understanding-package-manager-and-systemctl
tags: 90daysofdevops, 90daysofdevops-chanllenge

---

## What is a Package Manager?

A package manager in Linux is a software tool that simplifies the process of installing, updating, configuring, and removing software on a Linux-based operating system. It helps users and administrators manage software packages, which are collections of files and metadata that make up a particular piece of software. Package managers are crucial for maintaining a healthy and efficient Linux system, ensuring that software installations are straightforward, updates are timely, and potential conflicts between packages are minimized, ultimately enhancing the overall stability and security of the system.

Package managers save a lot of time and effort, and they also help to ensure that software is installed correctly and that all of its dependencies are met.

### **Various types of package managers**

There are two major types of package managers:

* **System-level package managers:** These package managers are responsible for managing all of the software packages on a system, including the operating system itself. System-level package managers are typically included with the operating system, and they are used to install, update, and remove all software packages.
    

Some examples of system-level package managers include:

* APT (Advanced Package Tool): Used by Ubuntu, Debian, and other Debian-based distributions.
    
* DNF (Dandified Yum): Used by Fedora and other Red Hat Enterprise Linux-based distributions.
    
* Pacman: Used by Arch Linux and Manjaro.
    
* Zypper: Used by openSUSE.
    
* Portage: Used by Gentoo Linux.
    
* **Application-level package managers:** These package managers are used to manage the dependencies of specific applications. Developers typically use application-level package managers to install and manage the libraries and other software components that their applications need.
    

Some examples of application-level package managers include:

* npm: Used to manage JavaScript packages.
    
* Yarn: Another JavaScript package manager.
    
* Bundler: Used to manage Ruby gems.
    
* Maven: Used to manage Java projects.
    
* Gradle: Another popular Java build tool.
    

The choice of package manager depends on the operating system, distribution, and software requirements. Each type of package manager offers unique features and benefits for software installation and management.

### systemctl

systemctl is a command-line tool and service management utility in Linux-based operating systems that is used to control and manage the services, daemons, and system units. It is a central component of the systemd init system, which has become the standard init system for many Linux distributions. Systemd is responsible for managing the initialization process and system services, replacing traditional init systems like SysVinit. systemctl is the primary interface for interacting with systemd.

### Task:

* You have to install docker and jenkins in your system from your terminal using package managers.
    

### **Update the package list and install the required dependencies:**

sudo apt update sudo apt install apt-transport-https ca-certificates curl software-properties-common

### Add Docker's official GPG key

curl -fsSL [https://download.docker.com/linux/ubuntu/gpg](https://download.docker.com/linux/ubuntu/gpg) | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

### **Docker Installation (using APT or Yum):**

Before we install the Docker engine on a machine for the first time, we need to set up the Docker repository, after which we can install and update the Docker from this repository we just set up.

**For Debian/Ubuntu (using APT):**

1. **Update the package database:**
    
    sudo apt update
    
2. **Install Docker using APT:**
    
    sudo apt install [docker.io](http://docker.io)
    

**For CentOS/RHEL (using Yum):**

1. **Install the EPEL repository for additional packages (if not already installed):**
    
    sudo yum install epel-release
    
2. **Install Docker using Yum:**
    
    sudo yum install docker
    
3. **Start and enable the Docker service:**
    
    sudo systemctl start docker
    
    sudo systemctl enable docker
    

### **Jenkins Installation (using APT or Yum):**

**For Debian/Ubuntu (using APT):**

1. **Add the Jenkins repository key to your system:**
    
    wget -q -O - [https://pkg.jenkins.io/debian/jenkins.io.key](https://pkg.jenkins.io/debian/jenkins.io.key) | sudo apt-key add -
    
2. **Add the Jenkins repository to your sources list:**
    
    sudo sh -c 'echo deb [http://pkg.jenkins.io/debian-stable](http://pkg.jenkins.io/debian-stable) binary/ &gt; /etc/apt/sources.list.d/jenkins.list'
    
3. **Update the package database:**
    
    sudo apt update
    
4. **Install Jenkins using APT:**
    
    sudo apt install jenkins
    

**For CentOS/RHEL (using Yum):**

1. **Create a Jenkins repository file:**
    
    sudo vi /etc/yum.repos.d/jenkins.repo
    
2. **Add the following repository configuration for Jenkins:**
    
    \[ jenkins \]
    
    name=Jenkins
    
    baseurl=[http://pkg.jenkins.io/redhat-stable/](http://pkg.jenkins.io/redhat-stable/) gpgcheck=1 gpgkey=[https://pkg.jenkins.io/redhat/jenkins.io.key](https://pkg.jenkins.io/redhat/jenkins.io.key)
    
3. **Install Jenkins using Yum:**
    
    sudo yum install jenkins
    
4. **Start and enable the Jenkins service:**
    
    sudo systemctl start jenkins
    
    sudo systemctl enable jenkins
    

### Task:

* Read about the commands systemctl vs service
    

systemctl status docker and service docker status are two different commands used to check the status of the Docker service on a Linux system. The choice of which command to use depends on your Linux distribution and its init system.

### systemctl status docker:

This command is used on Linux distributions that use systemd as their init system, such as Ubuntu 16.04 and newer, CentOS 7 and newer, and many others. It is used to query the status of a systemd-managed service, in this case, Docker. systemctl status docker gives detailed information about the Docker service's current status, including whether it's running, any recent log entries, and more.

### service docker status:

This command is used on Linux distributions that use the older SysVinit init system, such as Debian 7 (Wheezy) and older versions of Ubuntu. It queries the status of a service using the SysVinit service management system. This command typically provides a simple status message, such as "running" or "not running."

In most modern Linux distributions, you'll likely use systemctl status docker because they have transitioned to systemd as the default init system. However, if you are using an older distribution, you may need to use service docker status to check the status of the Docker service.
