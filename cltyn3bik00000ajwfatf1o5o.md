---
title: "Project-3: Hosting a static website using an AWS S3 bucket"
datePublished: Tue Mar 19 2024 17:19:29 GMT+0000 (Coordinated Universal Time)
cuid: cltyn3bik00000ajwfatf1o5o
slug: project-3-hosting-a-static-website-using-an-aws-s3-bucket
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710868550180/a7ffea14-51af-4da5-b762-e6b5eae3da77.png
tags: aws, devops, s3, 90daysofdevops

---

# Project Description

The project involves hosting a static website using an AWS S3 bucket. Amazon S3 is an object storage service that provides a simple web services interface to store and retrieve any amount of data. The website files will be uploaded to an S3 bucket and configured to function as a static website. The bucket will be configured with the appropriate permissions and a unique domain name, making the website publicly accessible. Overall, the project aims to leverage the benefits of AWS S3 to host and scale a static website in a cost-effective and scalable manner.

### **Create an S3 Bucket**

* Log in to the AWS Management Console and navigate to the S3 service.
    
* Click on “Create bucket”.
    
* Provide a unique bucket name.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710865071199/28552156-b89a-43a4-bb30-2bc4e0db31b6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710865541475/d5402deb-b2c0-4411-867f-a26eeb17772a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710865868766/77de600a-3c19-40fa-9343-1b5c61270ef4.png align="center")

* Click on “Create bucket”.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710865881465/4cf3fafb-e86f-4391-aed5-c33791223c6b.png align="center")

### **Upload Your Website Files**

* Open your newly created bucket.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710866170381/d92ef67a-b399-4500-a1ee-75e60e3f49c3.png align="center")

* Click on “Upload” and select your website files to upload them to the bucket.
    
* After selecting the files, click on “Upload”.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710866410275/2a32cc1d-0aa0-4daa-bf2d-bf87e1d5c1b5.png align="center")

### **Enable Static Website Hosting**

* Navigate to bucket properties and edit "Static website hosting".
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710867597136/61aeafa8-c12d-4f25-9540-8a71321d2855.png align="center")

### **Edit Block Public Access**

Uncheck “Block all public access” settings and acknowledge that so the bucket will be publicly accessible.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710867261377/b013da9d-130c-43c5-9ef2-9764f955b5a6.png align="center")

### **Set Bucket Permissions**

* In order to make the content publicly accessible, you need to modify the policy.
    
* Navigate to the Permission tab of your bucket, go to "Bucket policy" and click on "Edit"
    

```basic
{
     "Version": "2012-10-17",
     "Statement": [
         {
             "Sid": "PublicReadGetObject",
             "Effect": "Allow",
             "Principal": "*",
             "Action": "s3:GetObject",
             "Resource": "arn:aws:s3:::project-3-day-82/*"
         }
     ]
 }
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710867735437/ec7c1cf6-a9c4-44be-a104-b471cb238fd9.png align="center")

Click on "Save changes" to apply the policy.

### **Access Your Website**

* Upon successful configuration, your website should be reachable at the S3 endpoint URL.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710868224642/65d465ad-4360-487c-b79e-cfc201d0c08b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710868460038/4ef77913-6daa-4caa-bf48-beb83de74650.png align="center")

Thank you for reading.