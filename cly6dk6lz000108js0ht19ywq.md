---
title: "Automating User and Group Creation with a Bash Script"
datePublished: Wed Jul 03 2024 21:53:39 GMT+0000 (Coordinated Universal Time)
cuid: cly6dk6lz000108js0ht19ywq
slug: automating-user-and-group-creation-with-a-bash-script
tags: bash, bash-script, hnginternship, hng11

---

# Introduction

This technical article is about the creation of a bash script named create\_users.sh designed to automate user and group management on a Linux system. This script is part of the DevOps Stage 1 task for the HNG Internship. It reads a text file (user\_lists.txt) with employee usernames and their respective groups, creates the users and groups, sets up home directories with appropriate permissions and ownership, generates random passwords for the users, and logs all actions. The script also securely stores the generated passwords. By the end of this article, you'll understand the script's functionality.

### The Complete Script

```bash
#!/bin/bash

# Function to generate random password
generate_password() {
    openssl rand -base64 12
}

# Input file
input_file="user_lists.txt"

# Loop through each line in the input file
while IFS=';' read -r username groups; do
    # Check if username already exists
    if id "$username" &>/dev/null; then
        echo "User $username already exists. Skipping."
        echo "$(date) - User $username already exists. Skipping." >> /var/log/user_management.log
        continue
    fi

    # Create user and primary group
    useradd -m -s /bin/bash "$username"
    usermod -aG "$username" "$username"

    # Create additional groups
    IFS=',' read -ra groups_array <<< "$groups"
    for group in "${groups_array[@]}"; do
        groupadd "$group"
        usermod -aG "$group" "$username"
    done

    # Set password and log it securely
    password=$(generate_password)
    echo "$username:$password" | chpasswd
    echo "$(date) - Created user $username with groups $groups" >> /var/log/user_management.log
    echo "$username:$password" >> /var/secure/user_passwords.txt

    # Set permissions and ownership for home directory
    chown -R "$username:$username" "/home/$username"
    chmod 700 "/home/$username"

done < "$input_file"
```

Understanding the Script

Password Generation Function generates a random 12-character password.

```bash
generate_password() {
    openssl rand -base64 12
}
```

Input File defines the file with user and group information.

```bash
input_file="user_lists.txt"
```

This reads the file line-by-line, splitting into username and groups.

```bash
while IFS=';' read -r username groups; do
```

Check if the user exist and skips user creation if the user already exists.

```bash
if id "$username" &>/dev/null; then
    echo "User $username already exists. Skipping."
    echo "$(date) - User $username already exists. Skipping." >> /var/log/user_management.log
    continue
fi
```

User and Group Creation: Creates the user and primary group.

```bash
useradd -m -s /bin/bash "$username"
usermod -aG "$username" "$username"
```

Creates and assigns additional groups.

```bash
IFS=',' read -ra groups_array <<< "$groups"
for group in "${groups_array[@]}"; do
    groupadd "$group"
    usermod -aG "$group" "$username"
done
```

Sets the user’s password, logs the action, and stores the password securely.

```bash
password=$(generate_password)
echo "$username:$password" | chpasswd
echo "$(date) - Created user $username with groups $groups" >> /var/log/user_management.log
echo "$username:$password" >> /var/secure/user_passwords.txt
```

Sets ownership and permissions for the home directory.

```bash
chown -R "$username:$username" "/home/$username"
chmod 700 "/home/$username"
```

End of Loop

```bash
done < "$input_file"
```

Conclusion

This script allows SysOps engineers to efficiently manage employees' usernames and group names, ensuring security and consistency.

To learn more about the HNG program, visit the HNG Internship websites:

* [HNG Internship](https://hng.tech/internship)
    
* [HNG Hire](https://hng.tech/hire)