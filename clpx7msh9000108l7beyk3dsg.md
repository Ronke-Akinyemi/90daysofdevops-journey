---
title: "S3 Programmatic Access with AWS-CLI"
datePublished: Fri Dec 08 2023 22:40:08 GMT+0000 (Coordinated Universal Time)
cuid: clpx7msh9000108l7beyk3dsg
slug: s3-programmatic-access-with-aws-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702074940349/8c6299ca-0b51-4b8d-b436-9977f5b43bd5.png
tags: aws, learning-journey, devops-journey

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702067407722/ada402a4-8ba6-4e63-bb95-42853bbc40d6.png align="center")

Amazon Simple Storage Service (Amazon S3) is an object storage service that provides a secure and scalable way to store and access data on the cloud. It is designed for storing any kind of data, such as text files, images, videos, backups, and more. You can read more [HERE](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)

## Task-01

* Launch an EC2 instance using the AWS Management Console and connect to it using Secure Shell (SSH).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702068232107/dc558edb-a8b8-4a58-99ad-f1a2d4527294.png align="center")

Connect to your EC2 Instance using SSH:

```plaintext
ssh -i path/to/your-key-pair.pem ubuntu@[YOUR_EC2_PUBLIC_IP]
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702068464039/077fd3c8-d7c0-429b-94d2-09850b6fc8ac.png align="center")

* Create an S3 bucket and upload a file to it using the AWS Management Console.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702068869464/7223f104-323e-4934-b0a8-a64f236ad7b7.png align="center")

**Create a New S3 Bucket:** Click the "Create bucket" button and input a name for your bucket. Choose a region for your bucket. Configure the other options as needed. Then click "Create bucket."

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702069304036/a311d1c8-eab0-4ab1-90c1-09a1fe5c5846.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702069322688/d45f89a8-26ea-4d84-abf2-c5fea3b453dd.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702069337311/091dd702-4f35-40d8-b3e2-0df4f779dc80.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702069353024/bb94db0d-ca8a-477a-93cf-b0ba062283da.png align="center")

* Then click "Create bucket."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702069367651/e5ee2e4e-1f7d-4c9a-96ac-8a6849185739.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702069589675/9772e9a7-0079-46f2-bb6f-1e8e788a5b9a.png align="center")

* Once your bucket is created, click on its name to open it.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702069612516/ad3a9455-f40c-4cdb-92e6-08a034675efb.png align="center")

* Click the "Upload" button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702069823617/ff0f46ed-c323-4444-a237-83c1fe31aa57.png align="center")

* Click "Add files" and select the file you want to upload.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702069925281/c1721680-9bfb-4d8c-8689-9b558afb6b8d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702070166526/c9c80b0d-46fe-4e57-b5ac-1d5ac4058c85.png align="center")

* **Access the file from the EC2 instance using the AWS Command Line Interface (AWS CLI).**
    

**Install AWS CL**

```plaintext
sudo apt update
sudo apt install awscli
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702070444975/a3d324a2-5abe-4cc7-b691-16aafc3035b2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702070466038/36388c7f-04e5-449a-8fa9-02a8890020c1.png align="center")

**Configure AWS CLI:** Run `aws configure` and enter your AWS Access Key ID, Secret Access Key, region, and output format as prompted.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702070884205/fd469d3e-c0b8-4c6c-a10b-c23d0f830dd3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702070903222/e9d73add-394b-464e-a99e-53c3792b7672.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702071062437/27a75cae-5071-4ca2-8b7e-a6780a9c0d51.png align="center")

Use the `aws s3 cp` command to download the file from your S3 bucket to your EC2 instance.

```plaintext
aws s3 cp s3://BUCKET_NAME/PATH/TO/FILE /PATH/TO/LOCAL/FILE
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702071353467/ff4551e5-707e-4874-83c8-8e2b2e46529d.png align="center")

## Task-02

* Create a snapshot of the EC2 instance and use it to launch a new EC2 instance.
    
* Download a file from the S3 bucket using the AWS CLI.
    
* Verify that the contents of the file are the same on both EC2 instances.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702071787654/3120150c-7470-4e5f-836e-5af1a9ca033b.png align="center")

Choose "Snapshots" on the left hand side and click on "Create snapshot"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702072179723/c16c290d-7ab7-44b1-8847-a4b77e693032.png align="center")

Select the instance you want to create a snapshot of and click on Create snapshot

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702072659031/61e9a90b-44d7-4a65-b935-759a684b7faf.png align="center")

Use the newly created Snapshot to launch a new EC2 Instance: Click on "Actions" and select "Create image from snapshot". Follow the prompts to create an Amazon Machine Image (AMI) from your instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702072991915/ec09ea38-c425-4d3c-8ed1-539524700027.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702073008798/2baf63c0-3f11-406c-b9b2-167cd8da2c91.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702073028408/a7a1cbe6-5944-4c12-b17f-4127065d1f1a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702073371353/2b12ac9f-8019-4c2c-bccd-84ee39039df7.png align="center")

* In the EC2 Dashboard, select "AMIs" from the left-hand side, Choose the AMI you created in the previous step.
    
* Click "Launch Instance" and follow the instance creation instructions to launch a new instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702073548213/41f698cb-686c-4e6f-90a1-03656b678c9b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702073661687/6b2da73e-1086-4c65-93bf-4d52ca853b77.png align="center")

**Connect to the EC2 instance using SSH:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702074348945/844ec084-5f67-478c-9059-cc402bbc5e83.png align="center")

Connect as user "ubuntu"

```plaintext
ssh -i "Dev.pem" ubuntu@ec2-54-175-105-14.compute-1.amazonaws.com
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702073989790/6390d6cc-a66f-40df-adde-186d7813255b.png align="center")

* Download a file from the S3 bucket using the AWS CLI.
    
* Verify that the contents of the file are the same on both EC2 instances.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702074583072/a9018d9a-d547-4fdd-ade0-5b6312b4b570.png align="center")

### Here are some commonly used AWS CLI commands for Amazon S3:

`aws s3 ls` - This command lists all of the S3 buckets in your AWS account.

`aws s3 mb s3://bucket-name` - This command creates a new S3 bucket with the specified name.

`aws s3 rb s3://bucket-name` - This command deletes the specified S3 bucket.

`aws s3 cp file.txt s3://bucket-name` - This command uploads a file to an S3 bucket.

`aws s3 cp s3://bucket-name/file.txt .` - This command downloads a file from an S3 bucket to your local file system.

`aws s3 sync local-folder s3://bucket-name` - This command syncs the contents of a local folder with an S3 bucket.

`aws s3 ls s3://bucket-name` - This command lists the objects in an S3 bucket.

`aws s3 rm s3://bucket-name/file.txt` - This command deletes an object from an S3 bucket.

`aws s3 presign s3://bucket-name/file.txt` - This command generates a pre-signed URL for an S3 object, which can be used to grant temporary access to the object.

`aws s3api list-buckets` - This command retrieves a list of all S3 buckets in your AWS account, using the S3 API.