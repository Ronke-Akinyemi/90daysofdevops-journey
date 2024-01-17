---
title: "Python Libraries for DevOps"
datePublished: Fri Oct 27 2023 17:43:42 GMT+0000 (Coordinated Universal Time)
cuid: clo8wjs8q000609l49jwu8p6f
slug: python-libraries-for-devops
tags: python, devops, trainwithshubham, 90daysofdevops-chanllenge

---

## Reading JSON and YAML in Python

* As a DevOps Engineer, you should be able to parse files, be it txt, json, yaml, etc.
    
* You should know what libraries one should use in Python for DevOps.
    
* Python has numerous libraries like `os`, `sys`, `json`, `yaml` etc that a DevOps Engineer uses in day-to-day tasks.
    

### Tasks

1. Create a Dictionary in Python and write it to a JSON file
    

A JSON file is a file that contains data in JSON (JavaScript Object Notation) format. JSON files store structured data and are often used for configuration files, data exchange between different systems, and data storage. JSON files have the ".json" file extension. JSON files have a specific structure consisting of key-value pairs and can represent various data types, including strings, numbers, objects, arrays, booleans, and null values. JSON is human-readable, making it easy for humans and machines to work with.

* json.dump() - In Python, json.dump() is a method from the json module used to serialize (encode) a Python object and write it to a file-like object in JSON format. It is often used to save Python data as JSON in a file or other output stream.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698425633546/420f0bb2-d678-4511-a4e9-ef8228523341.png align="center")
    

1. Read a json file `services.json` kept in this folder and print the service names of every cloud service provider.Rear.d a json file `services.json` kept in this folder and print the service names of every cloud service provide
    

output

aws: ec2

azure: VM

gcp: compute engine

`json.loads()` is a Python method that is used to deserialize a JSON formatted string and convert it into a Python object. The term "loads" stands for "load string." This is commonly used to convert JSON data into a Python dictionary, list, or other appropriate data structure.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698427406929/006be58d-67c3-4286-ae9f-4dc28f0c04f0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698427432376/b7ea91d4-2749-4f13-aa42-191fea91d7f2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698427547141/d5d538c0-9e69-4f1e-8066-7b561cfeb036.png align="center")

1. Read YAML file using python, file `services.yaml` and read the contents to convert yaml to json
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698427585128/fba75994-bffc-407b-af34-190efc369a71.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698427605578/4aa58597-5f97-4716-a181-1374c01891d1.png align="center")

Thanks for reading!
