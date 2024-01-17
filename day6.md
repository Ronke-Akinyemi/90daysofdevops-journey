---
title: "File Permissions and Access Control Lists"
datePublished: Fri Oct 20 2023 00:06:11 GMT+0000 (Coordinated Universal Time)
cuid: clnxuouew000108mdaxgqhpw0
slug: file-permissions-and-access-control-lists
tags: devops, 90daysofdevops, trainwithshubham

---

File permissions and Access Control Lists (ACLs) are two mechanisms used in Unix-like operating systems to control and manage access to files and directories. They both play a crucial role in file security, but they differ in their complexity and capabilities.

File permissions are vital for controlling access to digital assets and safeguarding data. They are based on three categories: owner, group, and others, with three types of permissions - **read, write, and execute**. File permissions can be represented in symbolic and numeric notations. "chmod" is used to change the other users permissions of a file or directory.

| **Permission** | **Symbolic Notation** | **Numeric Notation** |
| --- | --- | --- |
| Read | r | 4 |
| Write | w | 2 |
| Execute | x | 1 |
| No Permission | \- | 0 |

In the symbolic notation:

* r stands for read permission.
    
* w stands for write permission.
    
* x stands for execute permission.
    
* \- indicates no permission for that particular category (user, group, and others).
    

In the numeric notation, each permission is assigned a numerical value, which can be added together to represent the overall permission level for a specific user category:

* 4 means to read permission.
    
* 2 means to write permission.
    
* 1 means to execute permission.
    
* 0 means to no permission.
    

To represent the overall permission for a file, you sum up the values of the permissions you want to grant. For example, if you want to grant read (4) and execute (1) permissions, you add them together, resulting in a numeric notation of 5.

Below are some examples of combined numeric notations for different permission levels:

* Read and Write (4 + 2) = 6
    
* Read, Write, and Execute (4 + 2 + 1) = 7
    
* Read and Execute (4 + 1) = 5
    
* No Permission (0)
    

You can use these numeric values to set permissions with the **chmod** command, making it a more concise way to manage file permissions in some cases.

### Access Control Lists (ACLs)

Access Control Lists provide a more fine-grained way to control access to files and directories.

Below are two important commands used in ACLs:

**getfacl:** This command is used to retrieve the ACL (Access Control List) for a file or directory. It displays detailed information about the ACL, including the users or groups with specific permissions.

**setfacl:** This command is used to set or modify the ACL for a file or directory. It allows you to grant or revoke specific permissions to specific users or groups.

### TASKS

Create a simple file and do `ls -ltr` to see the details of the files

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697756382089/a6501e52-5360-4d4c-8110-1c4a4bc3394c.jpeg align="center")

As a task, change the user permissions of the file and note the changes after `ls -ltr`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697756533321/6dc9d5b7-e86a-45de-9ac4-1546d3ebcf31.jpeg align="center")

Read about ACL and try out the commands getfacl and setfacl

You can use **getfacl** command to displays detailed information about the ACL

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697759820849/5feda141-6150-43ee-989e-c1759597ca3e.jpeg align="center")

Thanks for reading!
