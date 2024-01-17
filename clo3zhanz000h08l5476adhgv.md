---
title: "#90 DaysOfDevOps Challenge Day 12: Cheat Sheet  for  Linux & Git-GitHub"
datePublished: Tue Oct 24 2023 07:06:54 GMT+0000 (Coordinated Universal Time)
cuid: clo3zhanz000h08l5476adhgv
slug: 90-daysofdevops-challenge-day-12-cheat-sheet-for-linux-git-github
tags: github, git, linux-commands, trainwithshubham, 90daysofdevops-chanllenge

---

# Basic Linux Commands

## **Listing and directory commands**

**ls -l:** list the files and directories in a list format

**ls -a:** list all including hidden files and directories

**ls \*.sh** list all the files having .sh extension

**ls -d \*/:** list only directories

**pwd:** print work directories i.e gives the present working directory

**cd path\_to\_directory:** change the directory to the directory provided

**cd ~:** change the path to the home directory

**cd -:** go to the last working directory

**mkdir directoryName:** to make a directory in a specific location

## File Permissions

To view what's written in a file:

* **cat filename**
    

To change access permission of files:

* **chmod 777 folder\_name**
    

To grant full permissions to a directory and its contents:

* **chmod -R 777 directory\_name**
    

To remove the execution permission of any file:

* **chmod -x filename**
    

## User Management

To create new user:

* **sudo useradd newuser**
    

To set a password for a user:

* **sudo passwd newuser**
    

To view user information:

* **id username**
    

To delete a user:

* **sudo userdel username**
    

## Package Management

To install a package for Debian/Ubuntu-based systems:

* s**udo apt install package\_name**
    

To update a package for Debian/Ubuntu-based systems:

* **sudo apt update**
    

To remove a package for Debian/Ubuntu-based systems:

* **sudo apt remove package\_name**
    

## Git & GitHub Cheat Sheet

### Git Repository

To initialize a new git repository:

* **git init**
    

To clone an existing git repository:

* **git clone &lt;repository&gt;**
    

To add a file to the staging area:

* **git add &lt;file&gt;**
    

To commit changes:

* **git commit -m "commit message"**
    

To push changes to a remote repository:

* **git push origin &lt;branch\_name&gt;**
    

To pull changes from a remote repository:

* **git pull origin &lt;branch\_name&gt;**
    

### Branching and Merging

To create a new branch:

* **git branch &lt;new\_branch&gt;**
    

To merge branches:

* **git merge &lt;branch&gt;**
    

To list branches:

* **git branch**
    

To check the status of your repository:

* **git status**
    

To view commit history:

* **git log**
    

Thanks for reading!