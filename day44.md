---
title: "Relational Database Service in AWS"
datePublished: Sat Dec 09 2023 18:55:44 GMT+0000 (Coordinated Universal Time)
cuid: clpyf21s0000608joe648dkxw
slug: relational-database-service-in-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702147942694/2a770e04-decf-481d-8f66-cef5ea278e1f.png
tags: aws, devops, rds, devops-journey

---

Amazon Relational Database Service (Amazon RDS) is a collection of managed services that makes it simple to set up, operate, and scale databases in the cloud.

## Task-01: Create a Free tier RDS instance of MySQL

Go to the AWS Management Console, sign in, and go to the Amazon RDS service.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702141538649/aaa244b7-dd43-494b-adab-b7204b071d92.png align="center")

Click on "**Create database**" and choose "**MySQL**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702141585949/1f80b603-ac05-42d7-aac8-ded2818de17e.png align="center")

Select the "**Free tier**" template to ensure you are within the free tier limits.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702141683459/82a6079a-e0e1-46bb-a2ad-d6e72e09859a.png align="center")

Set up a "**master username**" and "**master password**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702141767187/1e20d0b4-3eed-403c-8d55-b22260841816.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702141995165/a300d51f-b5fa-4e65-a254-091397f1dbd7.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702142653684/ae89f06a-ad64-4f5b-a53b-eaad77fd8c4b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702142677782/37afb7c1-23b7-4199-a7ee-4a56ea4d7945.png align="center")

Then, click on "**Create database**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702142727383/11a9b1c1-1a36-496f-b7e7-de078d00e506.png align="center")

The database is created

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702142846180/6baf2ff0-9519-4e95-8b35-6be97d27abd9.png align="center")

* ### Create an EC2 instance
    
    Go to the EC2 service in the AWS Management Console.
    
    Click on "Instances" and then "Launch Instance".
    
    Choose an Amazon Machine Image (AMI)
    
    Select an instance type
    
    Configure the instance 
    
    Launch the instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702142966693/61891cc6-9054-4fe3-abc6-60d426e75224.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702143191233/7e5a5530-b82e-4769-90ff-041b20b9f545.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702143305863/9ecf09fc-b9fc-40b3-9727-78876963b94b.png align="center")

* ### Create an IAM role with RDS access
    
    Go to the **IAM** service in the AWS Management Console.
    
    Click on "**Roles**" and then "**Create role**".
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702143329052/f9f1ae69-c475-4404-ad4c-f0223b5562a0.png align="center")

Choose "**AWS service**" as the trusted entity type, select **EC2** as the use case, and click "**Next**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702143539407/60a4dd63-e432-4733-abc2-7985ee5a9dc9.png align="center")

Attach the policy `AmazonRDSFullAccess`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702145024426/26f94ea5-3004-4e97-b9ca-9e8f7a57eebc.png align="center")

Provide a name for the role.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702143620194/838cb3cc-e7de-45a4-b466-d8d1ccfe7a05.png align="center")

Then click "**Create role**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702145259217/2fca8fbd-d432-4f9b-8f55-156370854868.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702145400794/987f0da8-bd1f-42be-a48c-5006aca93c40.png align="center")

* ### Assign the role to EC2 so that your EC2 Instance can connect with RDS.
    
    Go back to the EC2 instance.
    
    Select the EC2 instance
    
    Under the "**Actions**" dropdown, go to "**Security**", and then "**Modify IAM Role**".
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702145418272/6b56d24d-79ea-451b-b149-43599003d143.png align="center")

Attach the IAM role you created to the EC2 instance and click "**Update IAM role**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702145588552/1a31c8fd-7ec5-48d1-a375-2826b0f03481.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702145686023/d064ed56-bf1b-4298-8b06-a404414c2e93.png align="center")

Connect your EC2 Instance with the RDS database

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702145863813/edf55eb1-222b-486b-87e2-234876ce9aeb.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702145883277/52a43623-6348-46cb-b7a0-1949d5e36a02.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702145902102/3de5d56f-8014-499c-aef9-3fd2e22c17dd.png align="center")

* ### Once the RDS instance is up and running, get the credentials and connect your EC2 instance using a MySQL client.
    

Select your RDS instance, and in the "**Connectivity & security**" tab, note the **endpoint**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702145919330/a3865f64-0b3e-4f39-a3a5-590cfa383837.png align="center")

SSH into your EC2 instance and **install mysql-client**:

```plaintext
sudo apt update
sudo apt install mysql-client
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702146342114/a0c617ba-e68e-4b87-ac76-b7e18f0f510d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702146406743/12633287-014b-469c-adab-d6cc87ff20e3.png align="center")

Now, to connect to the RDS instance using the MySQL client, we will use the command below:

```plaintext
mysql -h <endpoint-name> -P <port-name> -u <username> -p
```

Enter the password when prompted (the password we used when creating our MySQL database.)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702147092976/66c4700a-4797-4741-a7cb-96e483560786.png align="center")

We are now connected to our RDS instance from our EC2 instance using MySQL client.

Thank you...
