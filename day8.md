---
title: "Basic Git & GitHub for DevOps"
datePublished: Sat Oct 21 2023 17:40:04 GMT+0000 (Coordinated Universal Time)
cuid: clo0bs00s000309mj8ui82ky5
slug: basic-git-github-for-devops
tags: devops, 90daysofdevops, trainwithshubham, 90daysofdevops-chanllenge

---

# What is Git?

Git is a version control system that allows you to track changes to files and coordinate work on those files among multiple people. It is commonly used for software development, but it can be used to track changes to any set of files.

With Git, you can keep a record of who made changes to what part of a file, and you can revert to earlier versions of the file if needed. Git also makes it easy to collaborate with others, as you can share changes and merge the changes made by different people into a single version of a file.

## What is GitHub?

GitHub is a web-based platform that provides hosting for version control using Git. It is a subsidiary of Microsoft, and it offers all of the distributed version control and source code management (SCM) functionality of Git as well as adding its features. GitHub is a very popular platform for developers to share and collaborate on projects, and it is also used for hosting open-source projects.

## Differences between Git and GitHub

| **Feature** | **Git** | **GitHub** |
| --- | --- | --- |
| **Purpose** | Version control system | Web-based platform for hosting Git repositories and collaboration. |
| **Local vs. Remote** | Local (on your machine) | Remote (web-based hosting platform) |
| **Access and Collaboration** | Manual sharing of code, no built-in collaboration features. | Provides collaboration features like pull requests, issues, code reviews, and access control. |
| **Hosting** | No hosting, local version control system. | Hosts Git repositories on GitHub servers. |
| **Public vs. Private** | Repositories are private by default; you control visibility. | Supports both public (open to the world) and private repositories. |
| **Graphical User Interface** | Can use GUI tools, but the default interaction is through the command-line interface (CLI). | Provides a user-friendly web interface with graphical tools for managing repositories. |

**My GitHub Profile Overview**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697875128630/e678b69e-c74b-4454-ab8d-3db8ce780761.png align="center")

### What is Version Control?

Version control is a system that tracks and manages changes to files over time so that you can recall specific versions later. Version control is typically used in software development but applies to various fields where managing changes to documents or data is essential.

These are two main types of version control systems.

1. **Centralized Version Control System (CVCS):** In CVCS, there is a central server that stores the entire version history. Developers check out the files from this central repository, make changes, and then check them back in. Examples include Subversion (SVN) and Perforce.
    
2. **Distributed Version Control System (DVCS):** In DVCS, every developer has a complete copy of the repository, including the full history. This decentralized approach allows developers to work offline and is more resilient to server failures. Examples of DVCS include Git, Mercurial, and Dracs.
    

### Why do we use distributed version control system over centralized version control?

Distributed Version Control Systems (DVCS) offer several advantages over Centralized Version Control Systems (CVCS) that make them a preferred choice for many software development teams. Here are some of the key reasons why DVCS is favoured over CVCS:

1. Offline Access: In DVCS, each developer has a complete copy of the entire repository, so they can work offline, commit changes, and switch between branches without needing a network connection. In contrast, CVCS requires a constant connection to the central server for most operations.
    
2. Collaboration: DVCS enables more flexible and efficient collaboration. Developers can create local branches, make changes independently, and merge them back into the main branch. Collaboration promotes parallel development and minimizes conflicts.
    
3. Branching and Merging: DVCS systems excel at branching and merging. Developers can create branches quickly and merge them back into the main codebase with ease. This Branching and merging allows for experimentation, feature development, and bug fixes without disrupting the main branch.
    
4. Redundancy and Backup: Since every developer has a full copy of the repository, the risk of data loss is reduced. If the central server goes down, developers can continue working with their local copies and later push their changes when the server is back online.
    
5. Security: DVCS provides better security in terms of access control and permissions. Developers can work on their local copies without needing to write access to the central repository until their work is ready to be shared.
    
6. Faster Operations: Many operations in DVCS are faster because they are performed locally without the need for communication with a central server. This results in quicker commits, branch creation, and history browsing.
    
7. Flexibility: DVCS allows teams to choose their preferred workflows. Different developers can use different branching strategies, making it easier to accommodate a variety of development styles and project needs.
    

Thanks for reading!
